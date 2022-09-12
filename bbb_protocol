---
layout: page
title: "PROTOCOL"
permalink: /protocol/
---
			===========================================================
		     				The BBB protocol 
			===========================================================
	General guidelines:
		Each packet starts off with 0xBB and ends with 0x10|0x10
		packet format:
			0xBB|[Packet Type]|<CR>|<CR>
		
		Note:
			CR  =  0x10
			ETX =  0x03
		Things are enclosed in <>, eg <CR> just for emphasis.

	-----------------------------------------------------------
	service:
	-----------------------------------------------------------
		==register:==
		request:  REG_SERVICE[1 byte]|NAME|<CR>|<CR>
		response: REG_SERVICE_ACK[1 byte]|[Result][2 bytes]|ID[2 bytes]|<CR>|<CR>
			
			*Refer Appendix for Result
						
		==call_response:== 
		request: CALL[1 byte]|size|<CR>|DATA[size bytes]|<CR>|<CR>
		response: CALLRESP[1 byte]|[Result][2 bytes]|size|<CR>|DATA[size bytes]|<CR>|<CR>
			
			*Refer Appendix for Result
			*Service gets a request and responds with a response
				
		
		==stop_service:==
		request:
			STOP_SERVICE|<CR>
		response:
			STOP_SERVICE_ACK|[Result][2 bytes]|<CR>
			
			*Note: Stop service ACK will send OK only if all callers have stopped working. An internal queue will be maintained inside the service node that describes all active callers.
		
	

	
		
	----------------------------------------------------
	caller:
	----------------------------------------------------
		==register:==
		request: REG_CALLER[1 byte]|[SERVICE_NAME_A]|ETX|[SERVICE_NAME_B]|ETX|...|[SERVICE_NAME_N]<CR>|<CR>
		
		response:
			REG_CALLER_ACK[1 byte]|[Result][2 bytes]|ID[2 bytes]|SERV_ID_A[2 bytes]|SERV_ID_B[2 bytes]|...|<FF>|<FF>|<CR>|<CR>
				*Refer Appendix for Result
				*SERV_ID and ID are internally stored once a connection has been made and this information is not at all relevant in any way for the rest of the connection. 
				* Where FF is 0xFF in ascii [MAX number of CALLERS/SERVICEs = 2^16 - 1]
				* FF is reserved 
		
		==call==
			request:
				CALL[1 byte]|SERV_ID[2 bytes]|size|<CR>|DATA[size bytes]|<CR>|<CR>
			response:
				CALLRESP[1 bytes]|[Result][2 bytes]|size|<CR>|DATA[size bytes]|<CR>|<CR>
				
			*Caller issues a request and gets a response
		
		
		
		==stop caller==
			request:
				STOP_CALLER|<CR>
			response:
				STOP_CALLER_ACK|[Result][2 bytes]|<CR>
		



----------------Appendix---------------------------
	1. Result:
		NOTE: Result maybe OK or ERR
		if OK :
			Result = OK|OK_CODE
		if ERR:
			Result = ERR|ERR_CODE
			ID = 0x0000
	
	2. SIZE:
		NOTE : Size is specified in terms of ASCII numbers
		example:
			For a call with parameters having a size of 20
				`CALL|2|0|<CR>|[byte1]..[byte20]|<CR>|<CR>`	
	3.Further work:
		In Future versions, a checksum may be added at the end of each transmission.
	
	4. General guidelines:
			The general format is:
			REQID|(Result)|<CR>|size|DATA|<CR>|<CR>
	5. If the result in a CALLRESP or REG_[]_ACK is ERR
		all remaining fields (except for CR|CR at the end) shall be replaced by zero. Does not really matter though.
		
	6 . IMPORTANT NOTE
		NAME MUST CONTAIN ONLY ALPHANUMERICS NO _ NO - , NOTHING ELSE 



				---=============Deprecated====================--
	
	Deprecated because a caller must be able to call multiple services 
	----------------------------------------------------
	caller:
	----------------------------------------------------
		==register:==
		request: REG_CALLER[1 byte]|[SERVICE_NAME]|<CR>|<CR>
		
		response:
			REG_CALLER_ACK[1 byte]|[Result][2 bytes]|ID[2 bytes]|SERV_ID[2 bytes]|<CR>|<CR>
				*Refer Appendix for Result
				*SERV_ID and ID are internally stored once a connection has been made and this information is not at all relevant in any way for the rest of the connection. 
		
		
		==call==
			request:
				CALL[1 byte]|size|<CR>|DATA[size bytes]|<CR>|<CR>
			response:
				CALLRESP[1 bytes]|[Result][2 bytes]|size|<CR>|DATA[size bytes]|<CR>|<CR>
				
			*Caller issues a request and gets a response
		
		
		
		==stop caller==
			request:
				STOP_CALLER|
				CR>
			response:
				STOP_CALLER_ACK|[Result][2 bytes]|<CR>


```
