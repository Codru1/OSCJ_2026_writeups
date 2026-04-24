# Starting off
## Sunt accesate 2 platforme de social media de catre malware. Care sunt acestea?
Putem sa facem un educated guess si sa ne asumam ca platformele de social media sunt pe protocolul http
Daca aplicam filtrul http pe wireshark putem observa <br>
![fakebook](facebook.png) <br>
si <br>
![x](x.png) <br>
**Answer:OSC{facebook.com,x.com}** <br>
## Care este adresa IP a C2-ului?
Fiind un server C2 putem sa asumam ca va avea un volum ridicat de requesturi. Uitandune in statistici putem incerca IP-urile cu cele mai multe requesturi: <br>
![ips](ips.png) <br>
**Answer:OSC{147.45.44.42}** <br>
## Identificați numărul pachetului care contine transferul fisierului/payloadului adițional descarcat de malware.
Uitandude la File -> Export Objects -> HTTP putem vedea un fisier suspicous "Tricky.rar" <br>
![Tricky](Tricky.png) <br>
De aici puteam vedea numarul packetului ca fiind 69986 <br>
**Amswer:OSC{69986}** <br>
## Care este arrival time in pachetul ce contine fisierul .rar? <br>
Mergem la packetul cu numarul specificat precedant si vedem epotch arrival time 
![time.png](time.png) <br>
**Answer:OSC{1735330355.624480000}**<br>
## Ce "motiv" primeste C2-ul astfel incat sa autorizeze descarcarea malware-ului pe computerul infectat?
Uitandune in continuare in requesturile HTTP puteam vedea una care contine "?reason=..." <br>
![reason](reason.png)<br>
Tot requestul este: <br>

> /?reason=d29ya2VyNTk5Y2htZWw=:aWxvdmVpdA== <br>

De aici putea vedea ca **d29ya2VyNTk5Y2htZWw=** si **aWxvdmVpdA==** au egaluri la final ceea ce indica ca sunt base64 encoded <br>
Daca le decodam primim:
![decode1](decode1.png) <br>
si <br>
![decode1](decode2.png) <br>
**Answer:OSC{worker599chmel:iloveit}**

