---
title: CAN & vcan
parent: IO
---

generate at realistic rate \(from logged data\):  
  :  
```
   sudo modprobe vcan  
   sudo ip link add dev  type vcan  
   sudo ip link set up   
   while \(true\); do canplayer -I ; done  
```
TODO: Check commands versus original notes

 Collapse cantools decode:  
  `| cantools decode  | grep "^ " | awk '!/\(/ && last {print last} !/\(/ && last \|\| !/\(/ {print} /\(/{last=$0}' \| awk '//{printf "%s ",$0;next} 1'`  
TODO: Check commands versus original notes

 Start a vcan  
```
  sudo modprobe vcan  
  sudo ip link add dev  type vcan  
  sudo ip link set up   
```

 `vcan`  
  [https://elinux.org/Bringing\_CAN\_interface\_up](https://elinux.org/Bringing_CAN_interface_up)  
  Recommended <=500 frames/s on Beaglebone or similar  

 Decode CAN:  
   `| cantools decode  2> /dev/null`  

 List all signals from all dbc files  
  `ls *.dbc | xargs -I '{}' cantools dump '{}' | grep ^" +-- " | cut -d ' ' -f9 | sort | uniq | tee can_signals`  
TODO: Check commands versus original notes

 [https://elinux.org/Bringing\_CAN\_interface\_up](https://elinux.org/Bringing_CAN_interface_up)  
 [https://stackoverflow.com/questions/31328302/canplayer-wont-replay-candump-files](https://stackoverflow.com/questions/31328302/canplayer-wont-replay-candump-files)  
