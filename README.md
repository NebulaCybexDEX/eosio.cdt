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

trx json format
```
{
  "expiration": "2018-09-20T12:32:21",
  "ref_block_num": 15347,
  "ref_block_prefix": 1316674948,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [{
      "account": "redpacket.io",
      "name": "make",
      "authorization": [{
          "actor": "sunqi",
          "permission": "active"
        }
      ],
      "data": "0500000000000000000000000067a7c650c300000000000004535953000000000500000014000000"
    }
  ],
  "transaction_extensions": [],
  "signatures": [
    "SIG_K1_K5rLVc1pDX2m9zMQguVmECKYNttRsXkgBHRDg1aimF9hzaen49ycL6dA74Lb4Aobh2zdJqipDNHZF9NBfgLGZpa7bNurFZ"
  ],
  "context_free_data": []
}
```



##### take a red

```
cleos push action redpacket.io take '{"maker":"sunqi","taker":"holly2","id":5}' -p holly2
```
trx json format
```
{
  "expiration": "2018-09-20T12:32:21",
  "ref_block_num": 15347,
  "ref_block_prefix": 1316674948,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [{
      "account": "redpacket.io",
      "name": "take",
      "authorization": [{
          "actor": "holly2",
          "permission": "active"
        }
      ],
      "data": "00000000081f236d000000000067a7c60500000000000000"
    }
  ],
  "transaction_extensions": [],
  "signatures": [
    "SIG_K1_Km3t4WzrCEsunki9aUuP37Xh3kaZkoNPnpttQseH8gXtSiYnhs3YjUnfW7KF9eXxjKHLrCghSZUE4dCe1rhiiwLDMks2nt"
  ],
  "context_free_data": []
}
```

##### view

```
cleos push action redpacket.io view '{"maker":"sunqi","id":5}' -p sunqi
```
trx json format
```
{
  "expiration": "2018-09-20T12:32:21",
  "ref_block_num": 15347,
  "ref_block_prefix": 1316674948,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [{
      "account": "redpacket.io",
      "name": "view",
      "authorization": [{
          "actor": "sunqi",
          "permission": "active"
        }
      ],
      "data": "000000000067a7c60500000000000000"
    }
  ],
  "transaction_extensions": [],
  "signatures": [
    "SIG_K1_KVbKjpkXrwKRaxGQsjxsgjhFPmqwq5PAzMV3cm5AvZSHoF1YZFrjX9Pe1W4FDjxxAkJVCds16GL8bokR3wsyWugAU6Gyhj"
  ],
  "context_free_data": []
}
```

##### clear(reset, needs plt account permission)

```
 cleos push action redpacket.io clear '{"user":"redpacket.io"}' -p redpacket.io
```
trx json format
```
{
  "expiration": "2018-09-20T12:32:21",
  "ref_block_num": 15347,
  "ref_block_prefix": 1316674948,
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "context_free_actions": [],
  "actions": [{
      "account": "redpacket.io",
      "name": "clear",
      "authorization": [{
          "actor": "redpacket.io",
          "permission": "active"
        }
      ],
      "data": "401dc80a225393ba"
    }
  ],
  "transaction_extensions": [],
  "signatures": [
    "SIG_K1_K595GD7rud8Liv7nCeMY5Qykett2Dhekxp8wtGH7H21MHUChyLMatsH5US4Rr5CRnwy37Kr5UruQ9xNvqtyp3kXUksb7dH"
  ],
  "context_free_data": []
}
```


### redpacket ABI file
##### actions
```
        {
            "name": "clear",
            "base": "",
            "fields": [
                {
                    "name": "user",
                    "type": "name"
                }
            ]
        },
        {
            "name": "hi",
            "base": "",
            "fields": [
                {
                    "name": "user",
                    "type": "name"
                },
                {
                    "name": "memo",
                    "type": "string"
                }
            ]
        },
        {
            "name": "make",
            "base": "",
            "fields": [
                {
                    "name": "key",
                    "type": "uint64"
                },
                {
                    "name": "maker",
                    "type": "name"
                },
                {
                    "name": "pool",
                    "type": "asset"
                },
                {
                    "name": "people_num",
                    "type": "uint32"
                },
                {
                    "name": "expiration_time",
                    "type": "uint32"
                }
            ]
        },
        {
            "name": "take",
            "base": "",
            "fields": [
                {
                    "name": "taker",
                    "type": "name"
                },
                {
                    "name": "maker",
                    "type": "name"
                },
                {
                    "name": "id",
                    "type": "uint64"
                }
            ]
        },
        {
            "name": "view",
            "base": "",
            "fields": [
                {
                    "name": "maker",
                    "type": "name"
                },
                {
                    "name": "id",
                    "type": "uint64"
                }
            ]
        }
```
