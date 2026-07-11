# Lab 2: Infrastructure Redundancy & High Availability

## Installation & Configuration Steps

## Phase 1: Link Aggregation via LACP EtherChannel
1. Identify the redundant parallel physical uplinks connecting your Access Switches to the Distribution/Core Switch fabric.
2. Group the designated interface spans on both connecting nodes using the Cisco IOS command sequence:
   ```cfg
   interface range gigabitEthernet 0/1 - 2
   channel-group 1 mode active
