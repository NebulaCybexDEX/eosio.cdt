# prepare

## dependencies
please refer  https://github.com/eosio/eosio.cdt
download official toolkit source code, build and install to get eosio-cpp tool.

## build smart contract
```
cd redpacket
eosio-cpp -abigen redpacket.cpp -o redpacket.wasm
```
new files redpacket.cpp redpacket.wasm are generated.


# cybex SMCs (Smart Contracts)

## Redpacket

### create platform account 

```
cloes create account eosio redpacket.io <pubkey> <pubkey>
```
### set permission for plt account redpacket.io

```
cleos set account permission redpacket.io active '{"threshold": 1,"keys": [{"key": <pubkey>,"weight": 1}],"accounts": [{"permission":{"actor":"redpacket.io","permission":"eosio.code"},"weight":1}]}' owner -p redpacket.io
```

### set/load contract

```
cleos set contract redpacket.io <path>/redpacket -p redpacket.io
```

#### Actions

##### make a red

```
cleos push action redpacket.io make '{"key":5,"maker":"sunqi","pool":"5.0000 SYS","people_num":5,"expiration_time":20}' -
p sunqi
```

##### take a red

```
cleos push action redpacket.io take '{"maker":"sunqi","taker":"holly2","id":5}' -p holly2
```

##### view

```
cleos push action redpacket.io view '{"maker":"sunqi","id":5}' -p sunqi
```

##### clear(reset, needs plt account permission)

```
 cleos push action redpacket.io clear '{"user":"redpacket.io"}' -p redpacket.io
```

