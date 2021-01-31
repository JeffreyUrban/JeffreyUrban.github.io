---
title: CAN & vcan
parent: IO
---

# Decode CAN:

`... | cantools decode  2> /dev/null`

## Collapse cantools decode

```
... | cantools decode  | grep "^ " \
    | awk '!/(/ && last {print last} !/(/ && last \|\| !/(/ {print} /(/{last=$0}' \
    | awk '//{printf "%s ",$0;next} 1'
```

# List all signals from all dbc files

```
ls *.dbc | xargs -I '{}' cantools dump '{}' \
    | grep ^" +-- " | cut -d ' ' -f9 \
    | sort | uniq | tee can_signals
```

# vCAN

[Reference](https://elinux.org/Bringing_CAN_interface_up)

## Start a vcan  

```
sudo modprobe vcan  
sudo ip link add dev  type vcan  
sudo ip link set up   
```

_Recommended <=500 frames/s on Beaglebone or similar_

## Generate at realistic rate (from logged data)

```
 sudo modprobe vcan  
 sudo ip link add dev type vcan  
 sudo ip link set up   
 while (true); do canplayer -I ; done  
```

[Relevant discussion](https://stackoverflow.com/questions/31328302/canplayer-wont-replay-candump-files)
