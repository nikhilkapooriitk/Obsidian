-> Responsible for routing the PDU to the respective Bus Specific Interface Modules
-> Above the PduR module, all PDUs are protocol independent (Payload used instead of PDU id). Below PduR, PDUs are directed to protocol specific modules.
-> PduR interacts with COM, DCM, IPduM, LinIf, CanIf, CanNm, FrIf FrNm, CanTp, FrTp modules
![[Pasted image 20250625001854.png]]

Pdu Router routing table contains static PDU ids. PDU Ids are used to determine the destination of an IPdu.
![[Pasted image 20250625002432.png]]
Important functions of PduR:
- PDU reception from below modules and sending to DCM and COM
- PDU transmission from DCM, COM and sending to below modules
- PDU Gateway (send data from one comm protocol to other protocol (flexray to can frame))

##### IPDU Handling
Each Bsw Module that handles I-pdu (COM, canIf, PduR) contain a list of PDU Ids. PduR identifies the routing path by checking source I-PduID (located in PDUR configuration) and destination i-Pdu Id (located in destination module configuration).
Ex: If COM module transmits same i-pdu to canIf and LinIf. The PduR-ComTransmit is called. PduR will convert the source i-pdu id to one i-pdu id for LinIf ( LinIf module config) and one i-pdu id for canIf (canIf module config). PduInfoType value received from COM module is copied to the CanIF and LinIf modules without change.
![[Pasted image 20250625005155.png]]

##### 3 Ways to transmit PDUs:
1. **Top to bottom:** COM will call PduR_Tranmit( ipdu id ), then pduR will call CanIf_transmit( ipdu id). Data will be passed on from top to bottom layer.
2. **Bottom to Top:** Lower comm module requests transmission of i-pdu by calling pduR_TriggerTransmit() and PduR will forward that call to COM by calling COM_triggerTransmit(), then the data is copied by the upper module i.e., COM
3. **Mixed:** Com signal the transmit of data by PduR_Transmit(), but data is not copied now. Data will be copied when the lower layer call for PduR_triggerTransmit().
##### I-PDU Gateway Functionality
Support gatewaying from one source bus to multiple destination buses.
Gatewayed i-pdu can be transmitted up to COM module too.
Gateway can be done between interfaces (canIf -> LinIF) or TPs (CanTp -> LinTp) not mix.
2 ways of Gatewaying, depending on tag PduRDestiPduDataProvision:
1. If tag is PDUR_DIRECT: data will be directly copied to destination module.
2. If tag is TRIGGERTRANSMIT: data will be copied to a buffer in PduR module. Copied when the destination module calls PduR_TriggerTransmit().
