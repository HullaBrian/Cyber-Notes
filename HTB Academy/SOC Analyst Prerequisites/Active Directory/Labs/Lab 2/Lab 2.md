- Go to the windows search bar and enter `this pc`
![[Pasted image 20231210201227.png]]
- Click on the file with a check mark in the upper left hand corner
![[Pasted image 20231210201308.png]]
- Click `Change Settings` under the `Computer name, domain, and workgroup settings` section
![[Pasted image 20231210201429.png]]
- On the opened `System Properties window`, click the `Network ID...` button
- Make sure that the option describing the type of network says that it is part of a business network, then click next
- Make sure the `My company uses a network with a domain` option is selected then click next
- Click next again then enter in the given `htb-student_adm` credentials, making sure to enter in the `INLANEFREIGHT` domain as well
![[Pasted image 20231210202041.png]]
- Click next, then make sure that the computer name is `ACADEMY-IAD-W10` and the computer domain is `INLANEFREIGHT`
![[Pasted image 20231210202123.png]]
- After clicking next, enter in the domain users credentials and the desired domain
![[Pasted image 20231210202231.png]]
- Click `OK`

- Note that the Hack the Box Lab wants you to go back to the domain controller and move the computer to the proper `Analysts` OU, but since its a separate "lesson" you no longer can connect to the domain controller. I'm sure there's a way to do it, but since it's really not difficult to move the computer from the Computers OU to the proper `Analysts` OU, I decided not to do it.