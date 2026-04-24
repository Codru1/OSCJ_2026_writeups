# Starting off
##Sunt accesate 2 platforme de social media de catre malware. Care sunt acestea?
Putem sa facem un educated guess si sa ne asumam ca platformele de social media sunt pe protocolul http
Daca aplicam filtrul http pe wireshark putem observa 
![fakebook](facebook.png) <br>
si <br>
![x](x.png) <br>
**Answer:OSC{facebook.com,x.com}** <br>
##Care este adresa IP a C2-ului?
Fiind un server C2 putem sa asumam ca va avea un volum ridicat de requesturi. Uitandune in statistici putem incerca IP-urile cu cele mai multe requesturi: <br>
![ips](ips.png) <br>
**Answer:OSC{147.45.44.42}** <br>
