+++
author = "Thomas Evensen"
title = "Timer and Calendar"
date = "2025-03-01"
tags = ["timer"]
categories = ["technical details"]
+++

### The Timer and Calendar

The Calendar and schedules are developed by utilzing the Timer library. The actual synchronize task is kicked off when the scheduler writes the profile name to an observed value monitored by RsyncUI. The profile name is added to the schedule itself, the callback does the update of the observed value when the timer is kicked off. 

When RsyncUI observes that the value is updated, it trigger a URL-function in RsyncUI by using the profile name, the URL-function then kick off the actual synchronization task.  

If RsyncUI is alive, any update of the observed value will commence a synchronization task. The *weak spot* is how the Timer works and its limitations. 

#### The Timer code

The Timer is a Global static class with one task only, keep track of one timer which is the first timer to kick off. It also executes the callback function when the timer is kicked off. There are one other major part of the Calendar function, the object which calculates next time and display futures timers when there is an update.

The Calenderview asks the calendear object when the user views this and futures months. The Calendar view is dynamically updated, based on the input within the calendar table view.

The Global static timer only keeps track of one timer. 

To wrap it up, the Timer itself is very easy but with limitations. The calendar object is somewhat more complex, with two major tasks: 

- compute the next timer to execute and update the Global static timer
- provide the Calenderview with future times, computed only when the user browse the calendar

```swift
//
//  GlobalTimer.swift
//  Calendar
//
//  Created by Thomas Evensen on 31/03/2025.
//

import Foundation
import Observation
import OSLog

@Observable
final class GlobalTimer {
    @MainActor static let shared = GlobalTimer()

    private init() {}

    var timer: Timer?
    // Only used for message in SidebarMainView
    @ObservationIgnored var schedule: String?

    private var schedules: [String: (time: Date, callback: () -> Void)] = [:]

    func addSchedule(profile: String?, time: Date, callback: @escaping () -> Void) {
        if profile == nil {
            Logger.process.info("GlobalTimer: addSchedule() - profile Default at time \(time)")
            schedules["Default"] = (time, callback)

        } else if let profile {
            Logger.process.info("GlobalTimer: addSchedule() - profile \(profile) at time \(time)")
            schedules[profile] = (time, callback)
        }

        start()
    }

      func clearSchedules() {
        guard schedules.count > 0 else {
            Logger.process.info("GlobalTimer: clearSchedules() NO timer to invalidate")

            timer?.invalidate()
            timer = nil
            return
        }

        Logger.process.info("GlobalTimer: clearSchedules() and INVALIDATE old timer")

        schedules.removeAll()
        timer?.invalidate()
        timer = nil
    }

    private func start() {
        if timer == nil {
            Logger.process.info("GlobalTimer: start() new timer")

            timer = Timer.scheduledTimer(timeInterval: 60.0,
                                         target: self,
                                         selector: #selector(checkSchedules),
                                         userInfo: nil,
                                         repeats: true)
        }
    }

    @objc private func checkSchedules() {
        for (name, schedule) in schedules {
            Logger.process.info("GlobalTimer: checkSchedules(): Date.now \(Date.now) and schedule.time \(schedule.time)")

            if Date.now >= schedule.time {
                Logger.process.info("GlobalTimer: checkSchedules() - timer \(name) fired")

                schedule.callback()
            }
        }
    }
}
```
