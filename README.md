### P4 14: add --std p4-14

### Compile:

p4c --target bmv2 --arch v1model <File name>
  
p4c --target bmv2 --arch v1model my-p4-16-prog.p4

p4c --target bmv2 --arch v1model --std p4-14 my-p4-14-prog.p4

### Output p4runtime:

p4c --target bmv2 --arch v1model --p4runtime-files <p4runtime.txt> <p4program.p4>

p4c --target bmv2 --arch v1model --p4runtime-files my-p4-16-prog.p4info.txt my-p4-16-prog.p4

p4c --target bmv2 --arch v1model --p4runtime-files my-p4-14-prog.p4info.txt --std p4-14 my-p4-14-prog.p4


### Run mininet with simple_switch and .json configuration

sudo python <topo> --behavioral-exe simple_switch --json <file.json/compiled>
  
sudo python topo.py --behavioral-exe simple_switch --json p4include/mpls.json

### Run controller/flow rule writer

./install_flow_rules.sh

simple_switch_CLI --thrift-port 9090 < s1-commands

simple_switch_CLI --thrift-port 9091 < s2-commands

### File content:s1-commands

================================================================

table_add <name of table> <name of actions> <key match> => <action param1> <action param2> .....
  
table_add iplookup_table forward 10.0.10.10 => 1

table_add fec_table push_mpls 10.0.20.0/24 => 10

table_add switching_table rewrite_macs 2 => 00:00:00:00:01:02 00:00:00:00:02:01

================================================================
