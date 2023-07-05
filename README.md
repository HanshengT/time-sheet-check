# Time Sheet Check Tool

## Description
This is a simple calculating tool for converting batch of working start time and end time into total working hours.

## Usage
When you enter your start time and end time, it will show you the hour of the day and the total hours of multiple days.

For example:
- Entering `730` & `AM` for the start time and `545` & `PM` for the end time, it represents `7:30 AM` to `5:45 PM` and will return `10.25` hour as the result.
- Entering `9` & `AM` for the start time and `630` & `PM` for the end time, it represents `9:00 AM` to `5:45 PM` and will return `9.25` hour as the result.
- Entering both time above, total hours of `19.75` will be displayed.

Time formats supported: `["hhmm-A", "hmm-A", "h-A", "hh-A"]`. All time numbers are in 12 hours.