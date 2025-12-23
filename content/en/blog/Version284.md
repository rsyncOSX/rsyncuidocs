+++
author = "Thomas Evensen"
title = "Version 2.8.4"
date = "2025-12-21"
tags = ["changelog","version 2.8.4"]
categories = ["changelog"]
+++

### Version 2.8.4 - In Development (Build 175)

Version 2.8.4 is scheduled for release sometime later in December 2025, *the Changelog is compiled by AI*.
All notable changes to RsyncUI will be documented in this file.

In response to the significant modifications, a release candidate has been released. Below is a comprehensive changelog, highlighting the most notable change: the introduction of the *RsyncProcessStreaming* package. The primary objective of the new package is to maintain its simplicity and safety.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### Major Changes

#### RsyncProcessStreaming Migration - Complete Overhaul
- **Unified Process Execution**: Migrated entire codebase from legacy `RsyncProcess` to modern `RsyncProcessStreaming` package
- **Event-Driven Architecture**: Implemented streaming handlers with real-time output capture
  - Process output handler for live data streaming
  - Process termination handler for cleanup
- **Memory Management**: Resolved retain cycles with proper handler cleanup and weak reference patterns
- **Handler Lifecycle**: Simplified handler creation via `ProcessHandlers` factory with built-in cleanup hooks

#### New Testing Infrastructure
- **RsyncUITests Target**: Added comprehensive UI test suite
  - Argument validation tests
  - Deeplink URL handling tests
  - Configuration validation tests
  - Profile management tests

### Added

#### Features
- **Configuration Table View**: New table view in ProfileView showing all configurations per profile
- **Argument Validation**: Toggle for validating rsync arguments before execution
  - Added user-configurable setting: "Validate arguments"
  - Dry-run validation to check argument validity
  - Prevents execution of invalid argument combinations
- **Silent Stats Mode**: User setting to silence missing stats errors without stopping error counting
- **Improved Help Text**: Enhanced documentation for `--delete` parameter usage in UI

#### Code Quality & Documentation
- **Comprehensive Code Quality Analysis**: Added detailed analysis document
  - Zero force unwraps and force casts
  - Zero TODO/FIXME markers
  - Modern Swift concurrency throughout
  - Professional OSLog logging
- **Code Quality Reports**: Updated TODO.md with detailed technical roadmap

### Changed

#### UI/UX Improvements
- **Column Renaming**: Renamed table column from "Time executed" to "Time last" across multiple views
- **Profile Deletion UI**: Refactored profile deletion workflow for better user experience
- **Progress View**: Enhanced styling and layout for synchronization progress
- **ExecuteEstTasksView**: Various UI refinements and updates
- **Settings Views**: Improved code formatting and readability

#### Refactoring - Code Quality & Consistency

**Naming Conventions**:
- **Enum Cases**: Refactored all enum cases to use camelCase (Swift naming guidelines)
  - `RsyncCommand` enum cases
  - `PushPullCommand` enum cases
  - `OtherRsyncCommand` enum cases
  - `PlanSnapshots` enum case names
  - Day of week enums
- **Variable Names**: Standardized variable naming for clarity
  - Loop variable names improved
  - RemoteDataNumbers integer property names
  - FileManager variable naming consistency
  - Hidden ID handling improvements

**Code Organization**:
- **View Extensions**: Extracted complex view logic into separate extension files
  - TasksView toolbar → extension file
  - QuicktaskView toolbar and logic → extension file
  - SidebarMainView extension → separate file
  - AddTaskView logic → extension
- **SwiftLint Compliance**: Extensive SwiftLint cleanup
  - Removed inline line_length directives
  - Applied proper formatting rules
  - Added SwiftLint directives where appropriate
  - Updated .swiftlint.yml configuration

**Optional Handling**:
- Refactored optional handling patterns throughout codebase
- Improved guard statement ordering
- Safe optional unwrapping for URL and date creation
- Safe unwrapping of streamingHandlers before use

**Process Execution**:
- Refactored Estimate and Execute classes for streaming
- Simplified handler creation patterns
- Removed unnecessary `[weak self]` in termination handlers
- Refactored ObservableRestore to use RsyncProcessStreaming
- Updated task verification to use streaming process
- Rsync version check refactored to use streaming

**Configuration & Data Models**:
- Made parameter4 optional to better handle delete flag
- Use DefaultRsyncParameters enum for rsync flags
- Removed unused parameter1-3 from configuration models
- Refactored parameter fields to be optional
- Refactored default value assignment in RemoteDataNumbers

**Logging & Error Handling**:
- Refactored logging to use errorMessageOnly parameter
- Improved logging consistency throughout
- Silenced debug print statements in streaming handlers
- Gated per-line streaming logs behind DEBUG flag
- Enhanced stats error handling and alert threshold logic

**File Management**:
- Refactored log deletion to simplify parameters and usage
- Updated file headers and SwiftLint config
- Removed NSLocalizedString from UI labels (simplified)

### Removed
- **RsyncRealtimeView**: Removed obsolete real-time view and related UI references
- **Rsync Output Logfile Support**: Removed from log views (replaced by streaming)
- **RsyncProcess Dependency**: Fully migrated to RsyncProcessStreaming
- **Legacy Code**: Cleaned up unused code and test artifacts
- **Obsolete Parameters**: Removed unused parameter1-3 fields from configuration models

### Fixed
- **Guard Statement Order**: Fixed ordering and typos in snapshot and restore logic
- **Memory Leaks**: Released streaming references to prevent retain cycles
- **Nil Safety**: Added nil checks for arguments in executestreaming
- **Threading**: Added debug threading checks for streaming handlers
- **Actor Isolation**: Removed inappropriate @MainActor from TrimOutputFromRsync class
- **Typos**: Fixed typos and formatting issues in TasksView files
- **Deeplink Handling**: Refactored URL handling in SidebarMainView

### Dependencies
- **Swift Package Updates**: Multiple updates to Package.resolved
  - Updated RsyncProcessStreaming package revisions
  - Updated Swift package dependencies to main branch
  - Updated RsyncArguments package to branch v283
  - Updated RsyncProcess package to v283 branch

---

## [2.8.3] - December 12, 2025 (Build 174)

### Added
- **Silence Missing Stats**: New user-configurable setting to silence error alerts when rsync stats are missing
- **Error Control**: Improved user-configurable error handling for rsync operations

### Changed
- **Progress View**: Added vertical padding and compact ratio to progress columns
- **SwiftLint Configuration**: Updated rules and enforcement
- **Package Dependencies**: Updated all Swift packages to latest stable versions

### Fixed
- **Stats Handling**: Better handling of missing rsync statistics
- **Error Variable Naming**: Refactored error variable naming in catch blocks for consistency

---

## Version History Summary

### Development Timeline
- **v2.8.4** (In Development): Major streaming architecture overhaul, comprehensive testing
- **v2.8.3** (Dec 12, 2025): User-configurable error handling improvements
- **v2.8.2** (Dec 14, 2025): Configuration model enhancements

---

## Migration Notes

### From 2.8.2 to 2.8.4

#### Breaking Changes
None - backward compatible with existing configurations

#### New Features to Explore
1. **Argument Validation**: Enable in Settings → "Validate arguments"
2. **Silent Stats Mode**: Configure error handling in Settings
3. **Profile Configuration View**: View all configurations in ProfileView
4. **Improved Testing**: Enhanced reliability through comprehensive test coverage

#### Performance Improvements
- **Streaming Output**: Real-time progress updates without polling
- **Memory Management**: Improved handler lifecycle prevents leaks
- **Efficient Processing**: Event-driven architecture reduces overhead

---

## Development Philosophy

### Code Quality Principles
- **Safety First**: Zero force unwraps, zero force casts
- **Modern Swift**: Async/await, actors, @MainActor where appropriate
- **Professional Logging**: OSLog throughout, no print statements
- **Clean Architecture**: Clear separation of concerns
- **Automated Quality**: SwiftLint enforcement
- **Comprehensive Testing**: Unit and UI test coverage

### Ongoing Improvements
- Extracting output processing into reusable Swift Package
- Adding unit tests for output processing
- Introducing error telemetry hooks
- Extracting magic constants to centralized configuration
- Standardizing optional handling patterns

---

*For detailed technical documentation, see `AIDocuments/CODE_QUALITY_ANALYSIS_COMPREHENSIVE.md` and `AIDocuments/TODO.md`*

