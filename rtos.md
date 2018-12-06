<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>rtos</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__html"><h1 id="rtos-pour-k8">RTOS pour K8</h1>
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
<td align="center">(<a href="http://freertoshal.github.io">freertoshal.github.io</a>)[<a href="http://freertoshal.github.io/">http://freertoshal.github.io/</a>]</td>
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
<td align="center">?</td>
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
<td align="center">v</td>
<td align="center">X (event-driven)</td>
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
<h4 id="architecture">Architecture</h4>
<ul>
<li><code>task.c</code>&amp; <code>task.h</code></li>
<li><code>queue.c</code>&amp; <code>queue.h</code></li>
</ul>
<h5 id="task-states">Task states</h5>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-uMdeQHDNqZ4W8wu2" width="100%" style="max-width: 711.5px;" viewBox="0 0 711.5 451.5"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M323.671875,62.610868230202364L116.2578125,116.375L160.81840168095667,158.5" marker-end="url(#arrowhead9822)" style="fill:none"></path><defs><marker id="arrowhead9822" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M227.91796875,166.9049758048995L331.5859375,116.375L363.11315433212997,74.25" marker-end="url(#arrowhead9823)" style="fill:none"></path><defs><marker id="arrowhead9823" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M181.67778373194946,212.75L169.51171875,254.875L298.7890625,305.3969837753235" marker-end="url(#arrowhead9824)" style="fill:none"></path><defs><marker id="arrowhead9824" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M346.7109375,351.25L346.7109375,376.25L450.625,412.2047075143909" marker-end="url(#arrowhead9825)" style="fill:none"></path><defs><marker id="arrowhead9825" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M312.9316829309567,297L260.47265625,254.875L217.3068874097473,212.75" marker-end="url(#arrowhead9826)" style="fill:none"></path><defs><marker id="arrowhead9826" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M394.6328125,298.7240850923877L477.359375,254.875L477.359375,185.625L477.359375,116.375L420.2121361687726,74.25" marker-end="url(#arrowhead9827)" style="fill:none"></path><defs><marker id="arrowhead9827" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M497.359375,401.25L497.359375,376.25L497.359375,324.125L497.359375,254.875L227.91796875,194.26444473346953" marker-end="url(#arrowhead9828)" style="fill:none"></path><defs><marker id="arrowhead9828" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M544.09375,407.91625385473395L616.4296875,376.25L616.4296875,324.125L616.4296875,254.875L616.4296875,185.625L616.4296875,116.375L443.15625,64.87980285656809" marker-end="url(#arrowhead9829)" style="fill:none"></path><defs><marker id="arrowhead9829" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="translate(116.2578125,116.375)" style="opacity: 1;"><g transform="translate(-96.2578125,-17.125)" class="label"><foreignObject width="192.529541015625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">vTaskResume() called</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(331.5859375,116.375)" style="opacity: 1;"><g transform="translate(-99.0703125,-17.125)" class="label"><foreignObject width="198.150390625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">vTaskSuspend() called</span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(477.359375,185.625)" style="opacity: 1;"><g transform="translate(-99.0703125,-17.125)" class="label"><foreignObject width="198.150390625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">vTaskSuspend() called</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(497.359375,324.125)" style="opacity: 1;"><g transform="translate(-25.8984375,-17.125)" class="label"><foreignObject width="51.8023681640625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">event</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(616.4296875,254.875)" style="opacity: 1;"><g transform="translate(-99.0703125,-17.125)" class="label"><foreignObject width="198.150390625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">vTaskSuspend() called</span></div></foreignObject></g></g></g><g class="nodes"><g class="node" id="A" transform="translate(383.4140625,47.125)" style="opacity: 1;"><rect rx="5" ry="5" x="-59.7421875" y="-27.125" width="119.484375" height="54.25"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-49.7421875,-17.125)"><foreignObject width="99.4869384765625" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">suspended</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="B" transform="translate(189.51171875,185.625)"><rect rx="5" ry="5" x="-38.40625" y="-27.125" width="76.8125" height="54.25"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-28.40625,-17.125)"><foreignObject width="56.826171875" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Ready</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="C" transform="translate(346.7109375,324.125)"><rect rx="5" ry="5" x="-47.921875" y="-27.125" width="95.84375" height="54.25"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-37.921875,-17.125)"><foreignObject width="75.8505859375" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Running</div></foreignObject></g></g></g><g class="node" style="opacity: 1;" id="D" transform="translate(497.359375,428.375)"><rect rx="5" ry="5" x="-46.734375" y="-27.125" width="93.46875" height="54.25"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-36.734375,-17.125)"><foreignObject width="73.4827880859375" height="34.26041793823242"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Blocked</div></foreignObject></g></g></g></g></g></g></svg></div>
<h4 id="libs">Libs</h4>
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
<p>TinyOS et Contiki : non temps réels, très utilisés dans les réseaux de capteurs sans fils. FreeRTOS : pas de HAL … RIOT mise en avant pour sa programmiblité, efficacité énergétique. Référence à des librairies intégrées don <a href="http://cbor.io/">CBOR</a> qui pourrait concurrencer/supplenter le WOD <a href="http://cbor.io">http://cbor.io</a></p>
</blockquote>
<h4 id="hal-vs-api-"><a href="https://www.beningo.com/embedded-basics-apis-vs-hals/">HAL vs API </a></h4>
<h3 id="technologies--rencontrées">Technologies  rencontrées</h3>
<h4 id="cbor">CBOR</h4>
<p>Un format compact d’échange pour remplacer JSON dans des projets IoT, normé par l’IEFT.</p>
<ul>
<li><a href="https://en.wikipedia.org/wiki/CBOR">https://en.wikipedia.org/wiki/CBOR</a></li>
</ul>
</div>
</body>

</html>
