---
title: Binary Math
layout: post
description: Binary stuff
---

<!-- Hack 1: add a character display to text when 8 bits, determine if printable or not printable -->
<!-- Hack 2: change to 24 bits and add a color code and display color when 24 bits, think about display on this one -->
<!-- Hack 3: do your own thing -->



<div class="container bg-primary">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <span class="fs-4">Binary Math with Conversions</span>
    </header>
    <div class="row justify-content-md-center">
        <div class="col-8">
            <table class="table">
            <tr id="table">
                <th>Plus</th>
                <th>Binary</th>
                <th>Octal</th>
                <th>Hexadecimal</th>
                <th>Decimal</th>
                <th>Minus</th>
                <th>Change Bits</th>
            </tr>
            <tr>
                <td><button type="button" id="add1" onclick="add(1)">+1</button></td>
                <td id="binary">00000000</td>
                <td id="octal">0</td>
                <td id="hexadecimal">0</td>
                <td id="decimal">0</td>
                <td><button type="button" id="sub1" onclick="add(-1)">-1</button></td>
                <td><input type="input" id="addBit"></td>
            </tr>
            </table>
        </div>
        <div class="col-12" id="whereDaTable">
            <table class="table" id="bitHolder">
                <tr>
                    <td><img class="img-responsive py-3" id="bulb{{ i }}" src="{{site.baseurl}}/images/bulb_off.png" alt="" width="40" height="Auto">
                        <button type="button" id="butt{{ i }}" onclick="javascript:toggleBit({{ i }})">Turn on</button>
                    </td>
                </tr>
                <tr>
                    <td><input type='text' id="digit{{ i }}" Value="0" size="1" ></td>
                </tr>
            </table>
        </div>
    </div>
</div>

<script>
    const MSG_ON = "Turn on";
    const IMAGE_ON = "{{site.baseurl}}/images/bulb_on.gif";
    const MSG_OFF = "Turn off";
    const IMAGE_OFF = "{{site.baseurl}}/images/bulb_off.png";
    makeBits(1);
    const inp = document.getElementById("addBit");
    inp.addEventListener("keyup", function() {
        event.preventbase;
        if (event.key === "Enter") {
            makeBits(inp.value);
        }
    })// Thanks Aiden, XOXO


    function setBits(bitNum){
        var BITS = bitNum;
        console.log(BITS);
        var MAX = 2 ** BITS - 1;
        return [BITS, MAX];
    }
    // return string with current value of each bit
    function getBits() {
        let bits = "";
        for(let i = 0; i < BITS; i++) {
        bits = bits + document.getElementById('digit' + i).value;
        }
        return bits;
    }
    // setter for DOM values
    function setConversions(binary) {
        document.getElementById('binary').innerHTML = binary;
        // Octal conversion
        document.getElementById('octal').innerHTML = parseInt(binary, 2).toString(8);
        // Hexadecimal conversion
        document.getElementById('hexadecimal').innerHTML = parseInt(binary, 2).toString(16);
        // Decimal conversion
        document.getElementById('decimal').innerHTML = parseInt(binary, 2).toString();
    }
    //
    function decimal_2_base(decimal, base) {
        let conversion = "";
        // loop to convert to base
        do {
        let digit = decimal % base;
        conversion = "" + digit + conversion; // what does this do?
        decimal = ~~(decimal / base);         // what does this do?
        } while (decimal > 0);                  // why while at the end? what is ~~?
        // loop to pad with zeros
        if (base === 2) {                        // only pad for binary conversions
        for (let i = 0; conversion.length < BITS; i++) {
            conversion = "0" + conversion;
        }
        }
        return conversion;
    }

    // toggle selected bit and recalculate
    function toggleBit(i) {
        //alert("Digit action: " + i );
        const dig = document.getElementById('digit' + i);
        const image = document.getElementById('bulb' + i);
        const butt = document.getElementById('butt' + i);
        // Change digit and visual
        if (image.src.match(IMAGE_ON)) {
            dig.value = 0;
            image.src = IMAGE_OFF;
            butt.innerHTML = MSG_ON;
        } else {
            dig.value = 1;
            image.src = IMAGE_ON;
            butt.innerHTML = MSG_OFF;
        }
        // Binary numbers
        const binary = getBits();
        setConversions(binary);
    }
    // add is positive integer, subtract is negative integer
    function add(n) {
        let binary = getBits();
        // convert to decimal and do math
        let decimal = parseInt(binary, 2);
        if (n > 0) {  // PLUS
            decimal = MAX < decimal + n ? 0 : decimal += n; // OVERFLOW or PLUS
        } else  {     // MINUS
            decimal = 0 > decimal + n ? MAX : decimal += n; // OVERFLOW or MINUS
        }
        // convert the result back to binary
        binary = decimal_2_base(decimal, 2);
        // update conversions
        setConversions(binary);
        // update bits
        for (let i = 0; i < binary.length; i++) {
            let digit = binary.substr(i, 1);
            document.getElementById('digit' + i).value = digit;
            if (digit === "1") {
                document.getElementById('bulb' + i).src = IMAGE_ON;
                document.getElementById('butt' + i).innerHTML = MSG_OFF;
            } else {
                document.getElementById('bulb' + i).src = IMAGE_OFF;
                document.getElementById('butt' + i).innerHTML = MSG_ON;
            }
        }
    }
    // updates the html to change bits
    function makeBits(bitNum){
        BITS = setBits(bitNum)[0];
        MAX = setBits(bitNum)[1];
        document.getElementById("bitHolder").remove();
        const TABLE = document.createElement('table');
        TABLE.id = "bitHolder";
        whereDaTable.appendChild(TABLE);
        const row1 = TABLE.insertRow(0);
        for (let i = 0; i < bitNum; i++){
            var x = row1.insertCell(-1);
            var img = document.createElement('img');
            img.src = "{{site.baseurl}}/images/bulb_off.png";
            img.class = "img-responsive py-3";
            img.id = "bulb" + i;
            img.alt = "";
            img.width = "40";
            img.height = "95.63";
            x.appendChild(img);
            var btn = document.createElement('button')
            btn.type = "button";
            btn.id = "butt" + i;
            btn.onclick = function(){toggleBit(i)}
            btn.innerHTML = "Turn on";
            x.appendChild(btn);
        }
        const row2 = TABLE.insertRow(1)
        for (let i = 0; i < bitNum; i++){
            var x = row2.insertCell(-1);
            var input = document.createElement('input');
            input.id = "digit" + i;
            input.size = "1";
            input.readOnly = true;
            x.appendChild(input);
            document.getElementById("digit" + i).value = 0;
        }
        add(0);
    }
</script>
