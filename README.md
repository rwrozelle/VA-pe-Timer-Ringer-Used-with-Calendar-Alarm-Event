# VA-pe Timer Ringer Used with Calendar Alarm Event
This example is using a Local Calendar to store Alarm Events and then have them trigger the 'Timer Ringing" switch.

## Setup a Local Calendar
Create an Integration 'Local calendar' named 'HA Calendar'

## Externalize Timer Ringing in your VA-pes' script
Take control of your VA-pes and modify the switch 'Timer Ringing'.  There are different ways to do this.  
below is a recommendation by @jesserockz, after you take control, just add this to the bottom of the yaml.

```
switch:
  - id: !extend timer_ringing
    name: Timer Ringing
    internal: false
```
## Setup Timer Ringing switch
First, I hid each Timer Ringing switch.
Second, I renamed them "Timer Ringing", this ensures that the friendly_name is "Timer Ringing" as a state attribute.

## Setup Automations
Create 2 integrations 'Alarm-Set' and 'Alarm-Run'.  See automations folder

### Alarm-Set
This takes the time you provided and figures out a Start Date Time and End Date Time for the Calendar Event.  
The Description is the "{{trigger.device_id}}"
Figuring out Date Times is pretty rudimentary, but it works for alarms needed in the next 24 hours.

### Alarm-Run
When the Calendar Event in calendar 'HA Calendar' happens, the script using the description field to find the switch 'Timer Ringing' and turn it on.

## Testing
Make sure you set the calendar event at least 15 minutes into the future.
