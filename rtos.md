---


---

<h1 id="rtos-pour-k8">RTOS pour K8</h1>
<h2 id="introduction">Introduction</h2>
<p>Microcontrolleur de <a href="http://ww1.microchip.com/downloads/en/DeviceDoc/SAMD21-Family-DataSheet-DS40001882D.pdf">référence</a></p>
<h2 id="comparaison-rtos">Comparaison RTOS</h2>
<p>Autre <a href="https://www.osrtos.com/">listing</a></p>
<h3 id="tableau-de-comparaison-rtos--features">Tableau de comparaison RTOS / Features</h3>

<table>
<thead>
<tr>
<th>FEATURES/OS</th>
<th align="center">“Baremetal”</th>
<th align="center">FreeRTOS</th>
<th align="center">ARM Mbed</th>
<th align="center">RIOT</th>
<th align="center">Linux</th>
<th align="center">Contiki</th>
<th align="center">TinyOS</th>
<th align="center">Nucleus OS</th>
</tr>
</thead>
<tbody>
<tr>
<td>RT</td>
<td align="center">~</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center">~</td>
<td align="center"></td>
<td align="center"></td>
<td align="center">v</td>
</tr>
<tr>
<td>HAL</td>
<td align="center">~</td>
<td align="center"></td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>Modulaire</td>
<td align="center">~</td>
<td align="center">?X?</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center"></td>
<td align="center"></td>
<td align="center">?</td>
</tr>
<tr>
<td>Multi-thread</td>
<td align="center">~</td>
<td align="center">?</td>
<td align="center">?</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>C</td>
<td align="center">~</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center"></td>
<td align="center">~</td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>C++</td>
<td align="center">~</td>
<td align="center">?</td>
<td align="center">v</td>
<td align="center">v</td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
</tr>
<tr>
<td>min ROM</td>
<td align="center">~</td>
<td align="center">? &lt; 5-10ko ?</td>
<td align="center"></td>
<td align="center">~1.5ko</td>
<td align="center">~1mo</td>
<td align="center">&lt;2ko</td>
<td align="center">&lt;1ko</td>
<td align="center">?</td>
</tr>
<tr>
<td>min RAM</td>
<td align="center">~</td>
<td align="center">&lt;1ko</td>
<td align="center"></td>
<td align="center">~5ko</td>
<td align="center">~1mo</td>
<td align="center">&lt;2ko</td>
<td align="center">&lt;1kb</td>
<td align="center">?</td>
</tr>
<tr>
<td>Lib Bacnet</td>
<td align="center"><a href="https://www.softdel.com/bacnet-stack/">bacnet-stack MS/TP</a>, TODO</td>
<td align="center"><a href="https://www.softdel.com/bacnet-stack/">bacnet-stack MS/TP + I/P</a> TODO <a href="https://www.cimetrics.com/products/products-bacnet-ubacstac">uBacStack</a></td>
<td align="center"></td>
<td align="center">?</td>
<td align="center">?</td>
<td align="center">?</td>
<td align="center">?</td>
<td align="center">?</td>
</tr>
<tr>
<td>Lib SSL</td>
<td align="center">? WolfSSL ?</td>
<td align="center">WolfSSL</td>
<td align="center"></td>
<td align="center"><a href="https://github.com/RIOT-OS/RIOT/pull/6197">WolfSSL (alpha)</a></td>
<td align="center">wolfssl, openssl, openssh, …</td>
<td align="center">?</td>
<td align="center">WolfSSL</td>
<td align="center">WolfSSL</td>
</tr>
<tr>
<td>Lib CoAP</td>
<td align="center">?</td>
<td align="center">?</td>
<td align="center"></td>
<td align="center"><a href="https://github.com/RIOT-OS/RIOT/wiki/nanocoap-Home">nanocoap</a>,  <a href="https://github.com/RIOT-OS/RIOT/wiki/gcoap-Status">gcoap</a>, <a href="https://github.com/RIOT-OS/libcoap">lib-coap</a></td>
<td align="center">lib-coap</td>
<td align="center">lib-coap</td>
<td align="center">?</td>
<td align="center">?</td>
</tr>
<tr>
<td>Licence</td>
<td align="center"></td>
<td align="center">MIT</td>
<td align="center"></td>
<td align="center">LGPLv2.1</td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
<td align="center"></td>
</tr>
</tbody>
</table><h3 id="freertos">FreeRTOS</h3>
<h5 id="cartes-dévaluation">Cartes d’évaluation</h5>

<table>
<thead>
<tr>
<th>PORTs</th>
<th align="center">Compilateur</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="http://www.openrtos.net/Atmel_SAMD20_RTOS.html">ATMEL SAMD20</a></td>
<td align="center">Atmel Studio + GCC</td>
</tr>
<tr>
<td><a href="http://mcuoneclipse.wordpress.com/2012/09/29/tutorial-freedom-with-freertos-and-kinetis-l/">Kinetis ARM Cortex-M0+</a></td>
<td align="center">GCC - Eclise - CodeWarrior</td>
</tr>
<tr>
<td><a href="http://www.openrtos.net/Infineon-ARM-Cortex-M0-XMC1000-RTOS.html">XMC1000 ARM Cortex-M0</a></td>
<td align="center">IAR, Keil and GCC (using Atollic Eclipse project)</td>
</tr>
<tr>
<td><a href="http://www.openrtos.net/FreeRTOS-for-Cortex-M0-LPC1114-LPCXpresso.html">NXP LPC1114 LPCXpresso</a></td>
<td align="center">GCC, LPCXpresso IDE</td>
</tr>
<tr>
<td><a href="http://www.openrtos.net/FreeRTOS-for-STM32F051-Cortex-M0-IAR.html">STM32F0 ARM Cortex-M0</a></td>
<td align="center">IAR</td>
</tr>
<tr>
<td></td>
<td align="center"></td>
</tr>
</tbody>
</table><h3 id="articles-dintérêt">Articles d’intérêt</h3>
<h4 id="choosing-the-right-rtos-for-iot-plaform-target_blank"><a href="https://www.researchgate.net/publication/289253076_Choosing_the_right_RTOS_for_IoT_platform">Choosing the right RTOS for IOT plaform</a>{: target="_blank"}</h4>
<blockquote>
<p>Critères importants</p>
<ul>
<li>Modularité</li>
<li>Connectivité et interopérabilité, ex : POSIX</li>
</ul>
<p>TinyOS et Contiki : non temps réels, très utilisés dans les réseaux de capteurs sans fils. FreeRTOS : pas de HAL … RIOT mise en avant pour sa programmiblité, efficacité énergétique. Référence à des librairies intégrées don <a href="http://cbor.io/">CBOR</a> qui pourrait concurrencer/supplenter le WOD <a href="http://cbor.io/">http://cbor.io/</a></p>
</blockquote>
<h3 id="technologies--rencontrées">Technologies  rencontrées</h3>
<h4 id="cbor">CBOR</h4>
<p>Un format compact d’échange pour remplacer JSON dans des projets IoT, normé par l’IEFT.</p>
<ul>
<li><a href="https://en.wikipedia.org/wiki/CBOR">https://en.wikipedia.org/wiki/CBOR</a></li>
</ul>

