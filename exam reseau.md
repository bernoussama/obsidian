	1.
	```
	R1(config)#hostname R1
	R1(config)# enable secret Ofppt2024
	R1(config)# line vty 0 15
	R1(config-line)# 
	```

	7.
	`s2(config)#interface port-channel 1`
	`s2(config)# interface range fa0/1-2`
	`s2(config-if-range)# switchport mode trunk`
	`s2(config-if-range)# `