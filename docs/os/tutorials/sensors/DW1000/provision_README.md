<!--
#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing,
# software distributed under the License is distributed on an
# "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#  KIND, either express or implied.  See the License for the
# specific language governing permissions and limitations
# under the License.
#
-->

# Decawave provision example for provisioning

## Overview
Provision service allows tags/nodes to find the short addresses of all nodes of interest in its network. This is required for new nodes to iniitate rangeing and other communication with the other nodes in the network.

The DW1000 Device Driver Model contains the control plane for the provision packet transmissions and response receptions. The tags/nodes will send out a broadcast message and all the nodes are supposed to respond in a time slotted fashion. The new tag/node receives responses from other nodes in a sequence and stores their short address for future communication. The new tag/node continues to receive response messages from other nodes till receive timeout occurs. 

In this example apps(apps/tag_provision), a new tag(apps/tag_provision) initiates the the provisioning and all nearby nodes(apps/node_provision) respond to it. 

1. Build the Provision examples app

```no-highlight

newt target create node0
newt target set node0 app=apps/node_provision
newt target set node0 bsp=@mynewt-dw1000-core/hw/bsp/dwm1001
newt target set node0 build_profile=debug 
newt target amend node0 syscfg=DEVICE_ID=0x1111
newt target amend node0 syscfg=SLOT_ID=0
newt load node0
newt target amend node0 syscfg=DEVICE_ID=0x1112
newt target amend node0 syscfg=SLOT_ID=1
newt load node0
newt target amend node0 syscfg=DEVICE_ID=0x1113
newt target amend node0 syscfg=SLOT_ID=2
newt load node0
newt target amend node0 syscfg=DEVICE_ID=0x1114
newt target amend node0 syscfg=SLOT_ID=3
newt load node0

newt target create tag0
newt target set tag0 app=apps/tag_provision
newt target set tag0 bsp=@mynewt-dw1000-core/hw/bsp/dwm1001
newt target set tag0 build_profile=debug 
newt run tag0 0

```

