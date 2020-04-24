# SLP++ Electronic Contract Protocol Specification
### Specification version: 0.1
### Date published: April 24, 2020

### Requirements
**1. Need BSV genesis upgrade.**

# PROTOCOL DESCRIPTION

## Transaction Detail

### Create - Create Contract Transaction Outputs

This is the first transaction which defines the properties, metadata and contract self. 
```
The contract is identified by sha256 the create contract transaction outputscript which is referred as `contract_id`.
```

**Transaction inputs**: Any number of inputs or content of inputs, in any order.

**Transaction outputs**:
<table>
<tr>
  <td><b>v<sub>out</sub></b></td>
  <td><b>OutputScript </b></td>
  <td><b>BSV<br/>amount</b></td>
</tr>
  <tr>
    <td>...</td>
   <td>
   lockscript<sup>1</sup>: 'OP_DUP OP_HASH160 986b57ea26ff0081d4b555d28c OP_EQUALVERIFY OP_CHECKSIG' (0 to ∞ bytes)<br/>   
   OP_RETURN: '\x6a' (1 bytes, ascii)<br/>
   &lt;lokad_id: 'SLP++\x00'&gt; (6 bytes, ascii)<sup>2</sup><br/>
   &lt;type: 'contract/sotrage/vouchcher/source'&gt; (5 to 16 bytes ascii)<br/>
   &lt;action: 'CREATE'&gt; (6 bytes, ascii)<br/>
   &lt;title: &gt; (0 to 256 bytes, suggested utf-8)<br/>
   &lt;sign_date:&gt; (0 to 256 bytes, suggested utf-8)<br/>
   &lt;sign_exp_date&gt; (0 to 256 bytes, suggested ascii)<br/>
   &lt;exp_date&gt; (0 bytes or 256 bytes)<br/>
   &lt;mark:&gt; (0  to  1024 bytes, ascii)<br/>
   &lt;data_hash:&gt; (32 bytes)<br/>
   &lt;encrypt: '0' / '1'&gt; (1 byte integer)
   &lt;aes_pwd: (32 bytes ascii)
   &lt;pubkey1: &gt; (32 bytes ascii)
   &lt;pubkey2: &gt; (32 bytes ascii)
   </td>
    <td>any<sup>2</sup></td>
  </tr>
  
  <tr>
    <td>...</td>
    <td>Any</td>
    <td>any<sup>3</sup></td>
  </tr>
 
</table>

<sup>1. The lockscript can be any valid script combination.  MINT & SEND lockscript are the same means</sup>   

<sup>2. The Lokad identifier is registered as the number 0x504c532B2B (which, when encoded in the 6-byte little-endian format expected for Lokad IDs, gives the ascii string 'SLP++\x00'). Inquiries and additional information about the Lokad system of OP_RETURN protocol identifiers can be found at https://github.com/Lokad/Terab maintained by Joannes Vermorel.</sup>

<sup>3. SLP does not impose any restrictions on BSV output amounts. Typically however the OP_RETURN output would have 0 BSV (as any BSV sent would be burned), and outputs receiving tokens / mint batons would be sent only the minimal 'dust' amount of 0.00000546 BSV.</sup>

### UPdate - Update Contract Transaction Outputs

**Transaction outputs**:
<table>
<tr>
  <td><b>v<sub>out</sub></b></td>
  <td><b>OutputScript </b></td>
  <td><b>BSV<br/>amount</b></td>
</tr>
  <tr>
  <td>...</td>
  <td>
   lockscript: 'OP_DUP OP_HASH160 986b5779484a19fd99b555d28c OP_EQUALVERIFY OP_CHECKSIG'(0 to ∞ bytes)<br/>   
   OP_RETURN: '\x6a' (1 bytes, ascii)<br/>
&lt;lokad_id: 'SLP++\x00'&gt; (6 bytes, ascii)<BR>
&lt;type: 'contract/sotrage/vouchcher/source'&gt; (3 to 16 bytes ascii)<br/>
&lt;thransaction_type: 'REVOKE/REJECT/APPROVE'&gt; (5 to 16 byte ascii)<BR>
&lt;contract_id&gt; (32 bytes)<BR>
  </td>
    <td>any</td>
  </tr>

  <tr>
    <td>...</td>
    <td>Any</td>
    <td>any</td>
  </tr>

</table>


### Examples

**Create Contract Transaction**

bsv blockchain transaction:  a26d3191f2be3dc7fffdfa95ad7dc1bc3614079ebd626e0d87b20d2502682647

SCRIPT: ``006a04534c500001010747454e45534953045553445423546574686572204c74642e20555320646f6c6c6172206261636b656420746f6b656e734168747470733a2f2f7465746865722e746f2f77702d636f6e74656e742f75706c6f6164732f323031362f30362f546574686572576869746550617065722e70646620db4451f11eda33950670aaf59e704da90117ff7057283b032cfaec77793139160108010208002386f26fc10000``

SCRIPT BROKEN DOWN:
<table>
 <tr>
  <td>00</td>
  <td>OP_FALSE</td>
 <tr>
 <tr>
  <td>6a</td>
  <td>OP_RETURN</td>
 <tr>  
 <tr>
  <td>04</td>
  <td>length of lokad_id field (4 bytes)</td>
 <tr>
 <tr>
  <td>534c5000</td>
  <td>SLP\x00</td>
 <tr>
 <tr>
  <td>01</td>
  <td>length of token_type (1 byte)</td>
 <tr>
 <tr>
  <td>01</td>
  <td>token_type (1)</td>
 <tr>
 <tr>
  <td>07</td>
  <td>number of bytes in transaction_type (7 bytes)</td>
 <tr>
 <tr>
  <td>47454e45534953</td>
  <td>'GENESIS'</td>
 <tr>
 <tr>
  <td>04</td>
  <td>length of token_ticker (4 bytes)</td>
 <tr>
 <tr>
  <td>55534454</td>
  <td>'USDT'</td>
 <tr>
 <tr>
  <td>23</td>
  <td>length of token_name (35 bytes)</td>
 <tr>
 <tr>
  <td>
   546574686572204c74642e20555320646f6c6c61722062616<br/>
   36b656420746f6b656e73
  </td>
  <td>'Tether Ltd. US dollar backed tokens'</td>
 <tr>
 <tr>
  <td>41</td>
  <td>length of token_document_url (65 bytes)</td>
 <tr>
 <tr>
  <td>
   68747470733a2f2f7465746865722e746f2f77702d636f6e7<br/>
   4656e742f75706c6f6164732f323031362f30362f54657468<br/>
   6572576869746550617065722e706466
  </td>
  <td>'https://tether.to/wp-content/uploads/2016/06/TetherWhitePaper.pdf'</td>
 <tr>
 <tr>
  <td>20</td>
  <td>length of token_document_hash (32 bytes)</td>
 <tr>
 <tr>
  <td>
   db4451f11eda33950670aaf59e704da90117ff7057283b032<br/>
   cfaec7779313916
  </td>
  <td>token_document_hash</td>
 <tr>
 <tr>
  <td>01</td>
  <td>length for decimals (1 byte)</td>
 <tr>
 <tr>
  <td>08</td>
  <td>decimals (8)</td>
 <tr>
 <tr>
  <td>01</td>
  <td>length for mint_baton_vout (1 byte)</td>
 <tr>
 <tr>
  <td>02</td>
  <td>mint_baton_vout (2)</td>
 <tr>
 <tr>
  <td>08</td>
  <td>length of initial_token_mint_quantity (8 bytes)</td>
 <tr>
 <tr>
  <td>002386f26fc10000</td>
  <td>initial_token_mint_quantity (10,000,000,000,000,000)</td>
 </tr>
</table>

**Update Contract Transaction**

bsv blockchain transaction: 6b73adfbe7e5688c53ea4b09bf37de85dfd6dd4e3d38d1c0b4a5b38a9c0ca613

SCRIPT: ``006a04534c50000101044d494e5420a26d3191f2be3dc7fffdfa95ad7dc1bc3614079ebd626e0d87b20d2502682647010208002386f26fc10000``

SCRIPT BROKEN DOWN:
<table>
 <tr>
  <td>00</td>
  <td>OP_FALSE</td>
 </tr>
 <tr>
  <td>6a</td>
  <td>OP_RETURN</td>
 </tr>
 <tr>
  <td>04</td>
  <td>Length of lokad_id field (4 bytes)</td>
 </tr>
 <tr>
  <td>534c5000</td>
  <td>SLP\x00</td>
 </tr>
 <tr>
  <td>01</td>
  <td>length of token_type (1 byte)</td>
 </tr>
 <tr>
  <td>01</td>
  <td>token_type (1)</td>
 </tr>
 <tr>
  <td>04</td>
  <td>length of transaction_type field (4 bytes)</td>
 </tr>
 <tr>
  <td>4d494e54</td>
  <td>'MINT'</td>
 </tr>
 <tr>
  <td>20</td>
  <td>length of token_id (32 bytes)</td>
 </tr>
 <tr>
  <td>
   a26d3191f2be3dc7fffdfa95ad7dc1bc3614079ebd626e0d8<br/>
   7b20d2502682647
  </td>
  <td>token_id</td>
 </tr>
 <tr>
  <td>01</td>
  <td>length of mint_baton_vout (1 byte)</td>
 </tr>
 <tr>
  <td>02</td>
  <td>mint_baton_vout (2)</td>
 </tr>
 <tr>
  <td>08</td>
  <td>length of additional_token_quantity (8 bytes)</td>
 </tr>
 <tr>
  <td>002386f26fc10000</td>
  <td>additional_token_quantity (10,000,000,000,000,000)</td>
 </tr>
</table>

# Copyright

This protocol specification is published under the terms of the MIT license.