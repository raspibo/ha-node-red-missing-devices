# Home Assistant Node-RED check for missing devices

With this Node-RED flow and a Home Assistant automation you will be able to check if a device has gone missing.


## How it works

The Node-RED flow will periodically (every hour, by default) check every entity, groups them by devices and look for devices that have no entities updated since at least a given amount of time (by default, 12 hours).

If any is found, the `event_vanished_devices` event is triggered and the Home Assistant automation will notify the users.


## Installation

### Home Assistant automation

Open Home assistant, go to *Configuration, Automations and Scenes, Automations* and click *Add Automation*.

From there, click the menu (the three vertical dots on the top-right corner) and select *Edit in YAML*. In the text field, paste the content of the **ha-missing-devices-automation.yaml** file.


### Node-RED flow

Open Node-RED and import the **ha-node-red-missing-devices-flow.json** flow.


## Data structure received by the event


You can use the following items, from the `trigger.event.data` object.

```
{
  "topic": "vanished-devices",
  "vanishedDevicesString": "Kitchen Light, Garage Door",
  "numberOfVanishedDevices": 2,
  "payload": [
    {
      "device_id": "25ffdc66c8e492c8fe5a90764c1056e2",
      "device_name": "Kitchen Light",
      "last_updated": "2021-12-17T10:25:57.224Z"
    },
    {
      "device_id": "8c358946601611eca73c4f9016abe126",
      "device_name": "Garage Door",
      "last_updated": "2021-12-13T11:15:02.657Z"
    }
  ]
}
```

## FAQs

**How can I change the check interval?**

On Node-RED, edit the *periodic trigger* node.

**Home can I change the time used to consider a device as vanished?**

On Node-RED, edit the *check for inactive devices* node and change the `MAX_INACTIVITY_HOURS` constant.

**Home can I exclude a device by its ID or name?**

On Node-RED, edit the *check for inactive devices* node and edit the `SKIP_DEVICES_BY_ID` and/or `SKIP_DEVICES_BY_NAME` constants.

**Home can I receive a different kind of notifications?**

On Home Assistant, create an automation that is triggered by the `event_vanished_devices` event.


## Copyright and license

Copyright 2021 Davide Alberani <da@erlug.linux.it>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

