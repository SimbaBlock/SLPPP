# SLP++ Layer II Protocol List

 protocol `type`: 2 bytes integer, one byte for primary category, one byte for sub category field. 

### [common](./common)
```
  common: 0x01
     message: 0x01
     blockdrive: 0x02
     blog: 0x03
     wiki: 0x04
```

### [token](./token)
```
  token/payments: 0x02
     utility token: 0x01
     nft token: 0x02 	   
```

### [enterprise](./enterprise)
```
  enterprise: 0x03
     contract: 0x01
     project: 0x02
```

### [edu](./education)
```
  eduation: 0x04
     training: 0x01 
     mooc: 0x02    
     futureschool: 0x03
     book: 0x04
```
### [health](./health)
```
  health: 0x05
     ehr: 0x01
```  
For example, the type 0x0101 is [message](./common/slppp-message.md), the type 0x0301 is [contract](./enterprise/slppp-contract.md) etc.  