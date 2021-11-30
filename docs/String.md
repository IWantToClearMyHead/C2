### Emoji
Nowadays we have so many fun chars other than words, as below,
```
# cat f.c
#include <stdio.h>
#include <wchar.h>
#include <locale.h>

#define N 6

int main() {
  setlocale(LC_ALL, "en_US.utf-8");

  // Emoji array. Look up on emojipedia!
  wchar_t emojis[N] = {0x1f332, 0x1f341, 0x1f4cd, 0x1f342, 0x1f698, 0x1f387};

  // Print emoji array
  printf("This could be the description of any inspirational insta picture\n");
  printf("#reasontoroam #nrthwst\n");
  for(int i = 0; i < N; ++i) printf("%lc", emojis[i]);
  printf("\n");
}
root@hwsrv-894377:~# ./a.out 
This could be the description of any inspirational insta picture
#reasontoroam #nrthwst
🌲🍁📍🍂🚘🎇
```

The character developed in half century, 

| phase | coding  | note   |
|-------|---------|--------|
| 1     | ASCII   |        |
| 2     | ANSI    |        |
| 3     | GB2312  |        |
| 4     | GBK     |        |
| 5     | Unicode |        |
| 6     | UTF-16  |        |
| 7     | UTF-8   |        |

### UTF-8
The [UTF-8](https://www.fileformat.info/info/charset/UTF-8/list.htm) can be divided into several groups, as below

- Standard 0-255 Set
- Greek Characters
- General Punctuation
- Superscripts and Subscripts
- Currency Symbols
- Letterlike
- Fractions, Roman Numerals, etc.
- Arrows
- Geometric Shapes
- Block Symbols
- Math Operators and Symbols
- Control Pictures
- Enclosed Alphanumerics
- Box Drawing
- Block Elements
- Geometric Shapes
- Misc. Symbols
- Dingbats
- Misc. Symbols and Arrows
- Emoticons (U+1F600 to U+1F64F)
- Pictographs (Emojis) (U+1F300 to U+1F5FF)
- Transportation/Map
- Musical Symbols
- Domino Tiles
- Playing Cards
- Braille

Let's try to print a sun,
```
# cat g.c
#include <stdio.h>
#include <wchar.h>
#include <locale.h>

int main() {
  setlocale(LC_ALL, "en_US.utf-8");

  // Emoji array. Look up on emojipedia!
  wchar_t emojis = 127774; //\U0001F31E

  // Print emoji array
  printf("%lc\n", emojis);
}
# ./a.out 
🌞
```

### ASCII
Total number of Character in ASCII is 256 (0 to 255).
0 to 31(total 32 character) is called as ASCII control characters.
32 to 127 character is called as ASCII printable characters.
128 to 255 is called as The extended ASCII codes.

<table>
            <thead>
               <tr>
                  <td>Decimal</td>
                  <td>Octal</td>
                  <td>Hex</td>
                  <td>Binary</td>
                  <td>Value</td>
                  <td>Description</td>
               </tr>
            </thead>
            <tbody>
               <tr>
                  <td>000</td>
                  <td>000</td>
                  <td>00</td>
                  <td>0000 0000</td>
                  <td>NUL</td>
                  <td>"null" character</td>
               </tr>
               <tr>
                  <td>001</td>
                  <td>001</td>
                  <td>01</td>
                  <td>0000 0001</td>
                  <td>SOH</td>
                  <td>start of header</td>
               </tr>
               <tr>
                  <td>002</td>
                  <td>002</td>
                  <td>02</td>
                  <td>0000 0010</td>
                  <td>STX</td>
                  <td>start of text</td>
               </tr>
               <tr>
                  <td>003</td>
                  <td>003</td>
                  <td>03</td>
                  <td>0000 0011</td>
                  <td>ETX</td>
                  <td>end of text</td>
               </tr>
               <tr>
                  <td>004</td>
                  <td>004</td>
                  <td>04</td>
                  <td>0000 0100</td>
                  <td>EOT</td>
                  <td>end of transmission</td>
               </tr>
               <tr>
                  <td>005</td>
                  <td>005</td>
                  <td>05</td>
                  <td>0000 0101</td>
                  <td>ENQ</td>
                  <td>enquiry</td>
               </tr>
               <tr>
                  <td>006</td>
                  <td>006</td>
                  <td>06</td>
                  <td>0000 0110</td>
                  <td>ACK</td>
                  <td>acknowledgment</td>
               </tr>
               <tr>
                  <td>007</td>
                  <td>007</td>
                  <td>07</td>
                  <td>0000 0111</td>
                  <td>BEL</td>
                  <td>bell</td>
               </tr>
               <tr>
                  <td>008</td>
                  <td>010</td>
                  <td>08</td>
                  <td>0000 1000</td>
                  <td>BS</td>
                  <td>backspace</td>
               </tr>
               <tr>
                  <td>009</td>
                  <td>011</td>
                  <td>09</td>
                  <td>0000 1001</td>
                  <td>HT</td>
                  <td>horizontal tab</td>
               </tr>
               <tr>
                  <td>010</td>
                  <td>012</td>
                  <td>0A</td>
                  <td>0000 1010</td>
                  <td>LF</td>
                  <td>line feed</td>
               </tr>
               <tr>
                  <td>011</td>
                  <td>013</td>
                  <td>0B</td>
                  <td>0000 1011</td>
                  <td>VT</td>
                  <td>vertical tab</td>
               </tr>
               <tr>
                  <td>012</td>
                  <td>014</td>
                  <td>0C</td>
                  <td>0000 1100</td>
                  <td>FF</td>
                  <td>form feed</td>
               </tr>
               <tr>
                  <td>013</td>
                  <td>015</td>
                  <td>0D</td>
                  <td>0000 1101</td>
                  <td>CR</td>
                  <td>carriage return</td>
               </tr>
               <tr>
                  <td>014</td>
                  <td>016</td>
                  <td>0E</td>
                  <td>0000 1110</td>
                  <td>SO</td>
                  <td>shift out</td>
               </tr>
               <tr>
                  <td>015</td>
                  <td>017</td>
                  <td>0F</td>
                  <td>0000 1111</td>
                  <td>SI</td>
                  <td>shift in</td>
               </tr>
               <tr>
                  <td>016</td>
                  <td>020</td>
                  <td>10</td>
                  <td>0001 0000</td>
                  <td>DLE</td>
                  <td>data link escape</td>
               </tr>
               <tr>
                  <td>017</td>
                  <td>021</td>
                  <td>11</td>
                  <td>0001 0001</td>
                  <td>DC1</td>
                  <td>device control 1 (XON)</td>
               </tr>
               <tr>
                  <td>018</td>
                  <td>022</td>
                  <td>12</td>
                  <td>0001 0010</td>
                  <td>DC2</td>
                  <td>device control 2</td>
               </tr>
               <tr>
                  <td>019</td>
                  <td>023</td>
                  <td>13</td>
                  <td>0001 0011</td>
                  <td>DC3</td>
                  <td>device control 3 (XOFF)</td>
               </tr>
               <tr>
                  <td>020</td>
                  <td>024</td>
                  <td>14</td>
                  <td>0001 0100</td>
                  <td>DC4</td>
                  <td>device control 4</td>
               </tr>
               <tr>
                  <td>021</td>
                  <td>025</td>
                  <td>15</td>
                  <td>0001 0101</td>
                  <td>NAK</td>
                  <td>negative acknowledgement</td>
               </tr>
               <tr>
                  <td>022</td>
                  <td>026</td>
                  <td>16</td>
                  <td>0001 0110</td>
                  <td>SYN</td>
                  <td>synchronous idle</td>
               </tr>
               <tr>
                  <td>023</td>
                  <td>027</td>
                  <td>17</td>
                  <td>0001 0111</td>
                  <td>ETB</td>
                  <td>end of transmission block</td>
               </tr>
               <tr>
                  <td>024</td>
                  <td>030</td>
                  <td>18</td>
                  <td>0001 1000</td>
                  <td>CAN</td>
                  <td>cancel</td>
               </tr>
               <tr>
                  <td>025</td>
                  <td>031</td>
                  <td>19</td>
                  <td>0001 1001</td>
                  <td>EM</td>
                  <td>end of medium</td>
               </tr>
               <tr>
                  <td>026</td>
                  <td>032</td>
                  <td>1A</td>
                  <td>0001 1010</td>
                  <td>SUB</td>
                  <td>substitute</td>
               </tr>
               <tr>
                  <td>027</td>
                  <td>033</td>
                  <td>1B</td>
                  <td>0001 1011</td>
                  <td>ESC</td>
                  <td>escape</td>
               </tr>
               <tr>
                  <td>028</td>
                  <td>034</td>
                  <td>1C</td>
                  <td>0001 1100</td>
                  <td>FS</td>
                  <td>file separator</td>
               </tr>
               <tr>
                  <td>029</td>
                  <td>035</td>
                  <td>1D</td>
                  <td>0001 1101</td>
                  <td>GS</td>
                  <td>group separator</td>
               </tr>
               <tr>
                  <td>030</td>
                  <td>036</td>
                  <td>1E</td>
                  <td>0001 1110</td>
                  <td>RS</td>
                  <td>request to send/record separator</td>
               </tr>
               <tr>
                  <td>031</td>
                  <td>037</td>
                  <td>1F</td>
                  <td>0001 1111</td>
                  <td>US</td>
                  <td>unit separator</td>
               </tr>
               <tr>
                  <td>032</td>
                  <td>040</td>
                  <td>20</td>
                  <td>0010 0000</td>
                  <td>SP</td>
                  <td>space</td>
               </tr>
               <tr>
                  <td>033</td>
                  <td>041</td>
                  <td>21</td>
                  <td>0010 0001</td>
                  <td>!</td>
                  <td>exclamation mark</td>
               </tr>
               <tr>
                  <td>034</td>
                  <td>042</td>
                  <td>22</td>
                  <td>0010 0010</td>
                  <td>"</td>
                  <td>double quote</td>
               </tr>
               <tr>
                  <td>035</td>
                  <td>043</td>
                  <td>23</td>
                  <td>0010 0011</td>
                  <td>#</td>
                  <td>number sign</td>
               </tr>
               <tr>
                  <td>036</td>
                  <td>044</td>
                  <td>24</td>
                  <td>0010 0100</td>
                  <td>$</td>
                  <td>dollar sign</td>
               </tr>
               <tr>
                  <td>037</td>
                  <td>045</td>
                  <td>25</td>
                  <td>0010 0101</td>
                  <td>%</td>
                  <td>percent</td>
               </tr>
               <tr>
                  <td>038</td>
                  <td>046</td>
                  <td>26</td>
                  <td>0010 0110</td>
                  <td>&amp;</td>
                  <td>ampersand</td>
               </tr>
               <tr>
                  <td>039</td>
                  <td>047</td>
                  <td>27</td>
                  <td>0010 0111</td>
                  <td>'</td>
                  <td>single quote</td>
               </tr>
               <tr>
                  <td>040</td>
                  <td>050</td>
                  <td>28</td>
                  <td>0010 1000</td>
                  <td>(</td>
                  <td>left/opening parenthesis</td>
               </tr>
               <tr>
                  <td>041</td>
                  <td>051</td>
                  <td>29</td>
                  <td>0010 1001</td>
                  <td>)</td>
                  <td>right/closing parenthesis</td>
               </tr>
               <tr>
                  <td>042</td>
                  <td>052</td>
                  <td>2A</td>
                  <td>0010 1010</td>
                  <td>*</td>
                  <td>asterisk</td>
               </tr>
               <tr>
                  <td>043</td>
                  <td>053</td>
                  <td>2B</td>
                  <td>0010 1011</td>
                  <td>+</td>
                  <td>plus</td>
               </tr>
               <tr>
                  <td>044</td>
                  <td>054</td>
                  <td>2C</td>
                  <td>0010 1100</td>
                  <td>,</td>
                  <td>comma</td>
               </tr>
               <tr>
                  <td>045</td>
                  <td>055</td>
                  <td>2D</td>
                  <td>0010 1101</td>
                  <td>-</td>
                  <td>minus or dash</td>
               </tr>
               <tr>
                  <td>046</td>
                  <td>056</td>
                  <td>2E</td>
                  <td>0010 1110</td>
                  <td>.</td>
                  <td>dot</td>
               </tr>
               <tr>
                  <td>047</td>
                  <td>057</td>
                  <td>2F</td>
                  <td>0010 1111</td>
                  <td>/</td>
                  <td>forward slash</td>
               </tr>
               <tr>
                  <td>048</td>
                  <td>060</td>
                  <td>30</td>
                  <td>0011 0000</td>
                  <td>0</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>049</td>
                  <td>061</td>
                  <td>31</td>
                  <td>0011 0001</td>
                  <td>1</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>050</td>
                  <td>062</td>
                  <td>32</td>
                  <td>0011 0010</td>
                  <td>2</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>051</td>
                  <td>063</td>
                  <td>33</td>
                  <td>0011 0011</td>
                  <td>3</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>052</td>
                  <td>064</td>
                  <td>34</td>
                  <td>0011 0100</td>
                  <td>4</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>053</td>
                  <td>065</td>
                  <td>35</td>
                  <td>0011 0101</td>
                  <td>5</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>054</td>
                  <td>066</td>
                  <td>36</td>
                  <td>0011 0110</td>
                  <td>6</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>055</td>
                  <td>067</td>
                  <td>37</td>
                  <td>0011 0111</td>
                  <td>7</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>056</td>
                  <td>070</td>
                  <td>38</td>
                  <td>0011 1000</td>
                  <td>8</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>057</td>
                  <td>071</td>
                  <td>39</td>
                  <td>0011 1001</td>
                  <td>9</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>058</td>
                  <td>072</td>
                  <td>3A</td>
                  <td>0011 1010</td>
                  <td>:</td>
                  <td>colon</td>
               </tr>
               <tr>
                  <td>059</td>
                  <td>073</td>
                  <td>3B</td>
                  <td>0011 1011</td>
                  <td>;</td>
                  <td>semi-colon</td>
               </tr>
               <tr>
                  <td>060</td>
                  <td>074</td>
                  <td>3C</td>
                  <td>0011 1100</td>
                  <td>&lt; 
                  </td><td>less than</td>
               </tr>
               <tr>
                  <td>061</td>
                  <td>075</td>
                  <td>3D</td>
                  <td>0011 1101</td>
                  <td>=</td>
                  <td>equal sign</td>
               </tr>
               <tr>
                  <td>062</td>
                  <td>076</td>
                  <td>3E</td>
                  <td>0011 1110</td>
                  <td>&gt;</td>
                  <td>greater than</td>
               </tr>
               <tr>
                  <td>063</td>
                  <td>077</td>
                  <td>3F</td>
                  <td>0011 1111</td>
                  <td>?</td>
                  <td>question mark</td>
               </tr>
               <tr>
                  <td>064</td>
                  <td>100</td>
                  <td>40</td>
                  <td>0100 0000</td>
                  <td>@</td>
                  <td>"at" symbol</td>
               </tr>
               <tr>
                  <td>065</td>
                  <td>101</td>
                  <td>41</td>
                  <td>0100 0001</td>
                  <td>A</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>066</td>
                  <td>102</td>
                  <td>42</td>
                  <td>0100 0010</td>
                  <td>B</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>067</td>
                  <td>103</td>
                  <td>43</td>
                  <td>0100 0011</td>
                  <td>C</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>068</td>
                  <td>104</td>
                  <td>44</td>
                  <td>0100 0100</td>
                  <td>D</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>069</td>
                  <td>105</td>
                  <td>45</td>
                  <td>0100 0101</td>
                  <td>E</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>070</td>
                  <td>106</td>
                  <td>46</td>
                  <td>0100 0110</td>
                  <td>F</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>071</td>
                  <td>107</td>
                  <td>47</td>
                  <td>0100 0111</td>
                  <td>G</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>072</td>
                  <td>110</td>
                  <td>48</td>
                  <td>0100 1000</td>
                  <td>H</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>073</td>
                  <td>111</td>
                  <td>49</td>
                  <td>0100 1001</td>
                  <td>I</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>074</td>
                  <td>112</td>
                  <td>4A</td>
                  <td>0100 1010</td>
                  <td>J</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>075</td>
                  <td>113</td>
                  <td>4B</td>
                  <td>0100 1011</td>
                  <td>K</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>076</td>
                  <td>114</td>
                  <td>4C</td>
                  <td>0100 1100</td>
                  <td>L</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>077</td>
                  <td>115</td>
                  <td>4D</td>
                  <td>0100 1101</td>
                  <td>M</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>078</td>
                  <td>116</td>
                  <td>4E</td>
                  <td>0100 1110</td>
                  <td>N</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>079</td>
                  <td>117</td>
                  <td>4F</td>
                  <td>0100 1111</td>
                  <td>O</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>080</td>
                  <td>120</td>
                  <td>50</td>
                  <td>0101 0000</td>
                  <td>P</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>081</td>
                  <td>121</td>
                  <td>51</td>
                  <td>0101 0001</td>
                  <td>Q</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>082</td>
                  <td>122</td>
                  <td>52</td>
                  <td>0101 0010</td>
                  <td>R</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>083</td>
                  <td>123</td>
                  <td>53</td>
                  <td>0101 0011</td>
                  <td>S</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>084</td>
                  <td>124</td>
                  <td>54</td>
                  <td>0101 0100</td>
                  <td>T</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>085</td>
                  <td>125</td>
                  <td>55</td>
                  <td>0101 0101</td>
                  <td>U</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>086</td>
                  <td>126</td>
                  <td>56</td>
                  <td>0101 0110</td>
                  <td>V</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>087</td>
                  <td>127</td>
                  <td>57</td>
                  <td>0101 0111</td>
                  <td>W</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>088</td>
                  <td>130</td>
                  <td>58</td>
                  <td>0101 1000</td>
                  <td>X</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>089</td>
                  <td>131</td>
                  <td>59</td>
                  <td>0101 1001</td>
                  <td>Y</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>090</td>
                  <td>132</td>
                  <td>5A</td>
                  <td>0101 1010</td>
                  <td>Z</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>091</td>
                  <td>133</td>
                  <td>5B</td>
                  <td>0101 1011</td>
                  <td>[</td>
                  <td>left/opening bracket</td>
               </tr>
               <tr>
                  <td>092</td>
                  <td>134</td>
                  <td>5C</td>
                  <td>0101 1100</td>
                  <td>\</td>
                  <td>back slash</td>
               </tr>
               <tr>
                  <td>093</td>
                  <td>135</td>
                  <td>5D</td>
                  <td>0101 1101</td>
                  <td>]</td>
                  <td>right/closing bracket</td>
               </tr>
               <tr>
                  <td>094</td>
                  <td>136</td>
                  <td>5E</td>
                  <td>0101 1110</td>
                  <td>^</td>
                  <td>caret/circumflex</td>
               </tr>
               <tr>
                  <td>095</td>
                  <td>137</td>
                  <td>5F</td>
                  <td>0101 1111</td>
                  <td>_</td>
                  <td>underscore</td>
               </tr>
               <tr>
                  <td>096</td>
                  <td>140</td>
                  <td>60</td>
                  <td>0110 0000</td>
                  <td>`</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>097</td>
                  <td>141</td>
                  <td>61</td>
                  <td>0110 0001</td>
                  <td>a</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>098</td>
                  <td>142</td>
                  <td>62</td>
                  <td>0110 0010</td>
                  <td>b</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>099</td>
                  <td>143</td>
                  <td>63</td>
                  <td>0110 0011</td>
                  <td>c</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>100</td>
                  <td>144</td>
                  <td>64</td>
                  <td>0110 0100</td>
                  <td>d</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>101</td>
                  <td>145</td>
                  <td>65</td>
                  <td>0110 0101</td>
                  <td>e</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>102</td>
                  <td>146</td>
                  <td>66</td>
                  <td>0110 0110</td>
                  <td>f</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>103</td>
                  <td>147</td>
                  <td>67</td>
                  <td>0110 0111</td>
                  <td>g</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>104</td>
                  <td>150</td>
                  <td>68</td>
                  <td>0110 1000</td>
                  <td>h</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>105</td>
                  <td>151</td>
                  <td>69</td>
                  <td>0110 1001</td>
                  <td>i</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>106</td>
                  <td>152</td>
                  <td>6A</td>
                  <td>0110 1010</td>
                  <td>j</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>107</td>
                  <td>153</td>
                  <td>6B</td>
                  <td>0110 1011</td>
                  <td>k</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>108</td>
                  <td>154</td>
                  <td>6C</td>
                  <td>0110 1100</td>
                  <td>l</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>109</td>
                  <td>155</td>
                  <td>6D</td>
                  <td>0110 1101</td>
                  <td>m</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>110</td>
                  <td>156</td>
                  <td>6E</td>
                  <td>0110 1110</td>
                  <td>n</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>111</td>
                  <td>157</td>
                  <td>6F</td>
                  <td>0110 1111</td>
                  <td>o</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>112</td>
                  <td>160</td>
                  <td>70</td>
                  <td>0111 0000</td>
                  <td>p</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>113</td>
                  <td>161</td>
                  <td>71</td>
                  <td>0111 0001</td>
                  <td>q</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>114</td>
                  <td>162</td>
                  <td>72</td>
                  <td>0111 0010</td>
                  <td>r</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>115</td>
                  <td>163</td>
                  <td>73</td>
                  <td>0111 0011</td>
                  <td>s</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>116</td>
                  <td>164</td>
                  <td>74</td>
                  <td>0111 0100</td>
                  <td>t</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>117</td>
                  <td>165</td>
                  <td>75</td>
                  <td>0111 0101</td>
                  <td>u</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>118</td>
                  <td>166</td>
                  <td>76</td>
                  <td>0111 0110</td>
                  <td>v</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>119</td>
                  <td>167</td>
                  <td>77</td>
                  <td>0111 0111</td>
                  <td>w</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>120</td>
                  <td>170</td>
                  <td>78</td>
                  <td>0111 1000</td>
                  <td>x</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>121</td>
                  <td>171</td>
                  <td>79</td>
                  <td>0111 1001</td>
                  <td>y</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>122</td>
                  <td>172</td>
                  <td>7A</td>
                  <td>0111 1010</td>
                  <td>z</td>
                  <td>&nbsp;</td>
               </tr>
               <tr>
                  <td>123</td>
                  <td>173</td>
                  <td>7B</td>
                  <td>0111 1011</td>
                  <td>{</td>
                  <td>left/opening brace</td>
               </tr>
               <tr>
                  <td>124</td>
                  <td>174</td>
                  <td>7C</td>
                  <td>0111 1100</td>
                  <td>|</td>
                  <td>vertical bar</td>
               </tr>
               <tr>
                  <td>125</td>
                  <td>175</td>
                  <td>7D</td>
                  <td>0111 1101</td>
                  <td>}</td>
                  <td>right/closing brace</td>
               </tr>
               <tr>
                  <td>126</td>
                  <td>176</td>
                  <td>7E</td>
                  <td>0111 1110</td>
                  <td>~</td>
                  <td>tilde</td>
               </tr>
               <tr>
                  <td>127</td>
                  <td>177</td>
                  <td>7F</td>
                  <td>0111 1111</td>
                  <td>DEL</td>
                  <td>delete</td>
               </tr>
            </tbody>
         </table>

```
# cat a.c
#include <stdio.h>
int main( void )
{
        unsigned char char1 , char2 , char3 , char4 , char5 , char6 , char7 , char8 ;
        printf("|-------------------------------------------------------------------------------------------------------|\n" );
        printf("|                     ASCII table - excluding control characters                                        |\n" );
        printf("|-------------------------------------------------------------------------------------------------------|\n" );
        printf("|   Ch Dec  Hex  |  Ch Dec  Hex   | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex |\n" );
        printf("|----------------|----------------|-------------|-------------|-------------|-------------|-------------|\n" );
        for( int i = 0 ; i < 32; i++)
        {
                char1 = i;
                char2 = i+32;
                char3 = i+64;
                char4 = i+96;
                char5 = i+128; // extended ASCII characters
                char6 = i+160;
                char7 = i+192;
                char8 = i+224;
                printf( "|  %c    %3d %#x " ,
                                char2 , char2 , char2 );
                printf( "|  %c    %3d %#x " ,
                                char3 , char3 , char3 );
                if( char4 == 127 ) {
                        printf("|%s %3d %#x |" ,
                                        "DEL" , char4 , char4  );
                } else {
                        printf("|  %c %3d %#x |" ,
                                        char4 , char4 , char4  );
                }
                // Print extended ASCII for current system.
                printf("  %c %3d %#x |  %c %3d %#x |  %c %3d %#x |  %c %3d %#x |" ,
                                char5 , char5 , char5 ,
                                char6 , char6 , char6 ,
                                char7 , char7 , char7 ,
                                char8 , char8 , char8  );
                printf( "\n" );
        }
        printf("|-------------------------------------------------------------------------------------------------------|\n" );
}
# ./a.out
|-------------------------------------------------------------------------------------------------------|
|                     ASCII table - excluding control characters                                        |
|-------------------------------------------------------------------------------------------------------|
|   Ch Dec  Hex  |  Ch Dec  Hex   | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex | Ch Dec  Hex |
|----------------|----------------|-------------|-------------|-------------|-------------|-------------|
|        32 0x20 |  @     64 0x40 |  `  96 0x60 |  � 128 0x80 |  � 160 0xa0 |  � 192 0xc0 |  � 224 0xe0 |
|  !     33 0x21 |  A     65 0x41 |  a  97 0x61 |  � 129 0x81 |  � 161 0xa1 |  � 193 0xc1 |  � 225 0xe1 |
|  "     34 0x22 |  B     66 0x42 |  b  98 0x62 |  � 130 0x82 |  � 162 0xa2 |  � 194 0xc2 |  � 226 0xe2 |
|  #     35 0x23 |  C     67 0x43 |  c  99 0x63 |  � 131 0x83 |  � 163 0xa3 |  � 195 0xc3 |  � 227 0xe3 |
|  $     36 0x24 |  D     68 0x44 |  d 100 0x64 |  � 132 0x84 |  � 164 0xa4 |  � 196 0xc4 |  � 228 0xe4 |
|  %     37 0x25 |  E     69 0x45 |  e 101 0x65 |  � 133 0x85 |  � 165 0xa5 |  � 197 0xc5 |  � 229 0xe5 |
|  &     38 0x26 |  F     70 0x46 |  f 102 0x66 |  � 134 0x86 |  � 166 0xa6 |  � 198 0xc6 |  � 230 0xe6 |
|  '     39 0x27 |  G     71 0x47 |  g 103 0x67 |  � 135 0x87 |  � 167 0xa7 |  � 199 0xc7 |  � 231 0xe7 |
|  (     40 0x28 |  H     72 0x48 |  h 104 0x68 |  � 136 0x88 |  � 168 0xa8 |  � 200 0xc8 |  � 232 0xe8 |
|  )     41 0x29 |  I     73 0x49 |  i 105 0x69 |  � 137 0x89 |  � 169 0xa9 |  � 201 0xc9 |  � 233 0xe9 |
|  *     42 0x2a |  J     74 0x4a |  j 106 0x6a |  � 138 0x8a |  � 170 0xaa |  � 202 0xca |  � 234 0xea |
|  +     43 0x2b |  K     75 0x4b |  k 107 0x6b |  � 139 0x8b |  � 171 0xab |  � 203 0xcb |  � 235 0xeb |
|  ,     44 0x2c |  L     76 0x4c |  l 108 0x6c |  � 140 0x8c |  � 172 0xac |  � 204 0xcc |  � 236 0xec |
|  -     45 0x2d |  M     77 0x4d |  m 109 0x6d |  � 141 0x8d |  � 173 0xad |  � 205 0xcd |  � 237 0xed |
|  .     46 0x2e |  N     78 0x4e |  n 110 0x6e |  � 142 0x8e |  � 174 0xae |  � 206 0xce |  � 238 0xee |
|  /     47 0x2f |  O     79 0x4f |  o 111 0x6f |  � 143 0x8f |  � 175 0xaf |  � 207 0xcf |  � 239 0xef |
|  0     48 0x30 |  P     80 0x50 |  p 112 0x70 |  � 144 0x90 |  � 176 0xb0 |  � 208 0xd0 |  � 240 0xf0 |
|  1     49 0x31 |  Q     81 0x51 |  q 113 0x71 |  � 145 0x91 |  � 177 0xb1 |  � 209 0xd1 |  � 241 0xf1 |
|  2     50 0x32 |  R     82 0x52 |  r 114 0x72 |  � 146 0x92 |  � 178 0xb2 |  � 210 0xd2 |  � 242 0xf2 |
|  3     51 0x33 |  S     83 0x53 |  s 115 0x73 |  � 147 0x93 |  � 179 0xb3 |  � 211 0xd3 |  � 243 0xf3 |
|  4     52 0x34 |  T     84 0x54 |  t 116 0x74 |  � 148 0x94 |  � 180 0xb4 |  � 212 0xd4 |  � 244 0xf4 |
|  5     53 0x35 |  U     85 0x55 |  u 117 0x75 |  � 149 0x95 |  � 181 0xb5 |  � 213 0xd5 |  � 245 0xf5 |
|  6     54 0x36 |  V     86 0x56 |  v 118 0x76 |  � 150 0x96 |  � 182 0xb6 |  � 214 0xd6 |  � 246 0xf6 |
|  7     55 0x37 |  W     87 0x57 |  w 119 0x77 |  � 151 0x97 |  � 183 0xb7 |  � 215 0xd7 |  � 247 0xf7 |
|  8     56 0x38 |  X     88 0x58 |  x 120 0x78 |  � 152 0x98 |  � 184 0xb8 |  � 216 0xd8 |  � 248 0xf8 |
|  9     57 0x39 |  Y     89 0x59 |  y 121 0x79 |  � 153 0x99 |  � 185 0xb9 |  � 217 0xd9 |  � 249 0xf9 |
|  :     58 0x3a |  Z     90 0x5a |  z 122 0x7a |  � 154 0x9a |  � 186 0xba |  � 218 0xda |  � 250 0xfa |
|  ;     59 0x3b |  [     91 0x5b |  { 123 0x7b |  � 155 0x9b |  � 187 0xbb |  � 219 0xdb |  � 251 0xfb |
|  <     60 0x3c |  \     92 0x5c |  | 124 0x7c |  � 156 0x9c |  � 188 0xbc |  � 220 0xdc |  � 252 0xfc |
|  =     61 0x3d |  ]     93 0x5d |  } 125 0x7d |  � 157 0x9d |  � 189 0xbd |  � 221 0xdd |  � 253 0xfd |
|  >     62 0x3e |  ^     94 0x5e |  ~ 126 0x7e |  � 158 0x9e |  � 190 0xbe |  � 222 0xde |  � 254 0xfe |
|  ?     63 0x3f |  _     95 0x5f |DEL 127 0x7f |  � 159 0x9f |  � 191 0xbf |  � 223 0xdf |  � 255 0xff |
|-------------------------------------------------------------------------------------------------------|
```

Why is extended not shown? It's because the current locale not supported.
```
# cat a.c
#include <stdio.h>
#include <ctype.h>
#include <locale.h>
#include <limits.h>

static void print_char_page(const char *locale, int max)
{
int c;
char *loc;

if (NULL != (loc = setlocale(LC_CTYPE, NULL)) )
{
printf("locale changed from '%s', ", loc);
}

if (NULL != (loc = setlocale(LC_CTYPE, locale)) )
{
printf("to: '%s'\n", loc);
}

printf("+----+-----+---+\n");
printf("|Hex | Dec |Car|\n");
printf("+----+-----+---+\n");
for (c=0; c<max; c++)
{
if ( isprint(c) )
{
printf("| %02x | %3d | %c |\n", c, c, c);
}
}
}

int main(void)
{
/* change env to locale-specific native environment.*/
print_char_page("", UCHAR_MAX);

return 0;
}
# ./a.out
locale changed from 'C', to: 'C.UTF-8'
+----+-----+---+
|Hex | Dec |Car|
+----+-----+---+
| 20 |  32 |   |
| 21 |  33 | ! |
| 22 |  34 | " |
| 23 |  35 | # |
| 24 |  36 | $ |
| 25 |  37 | % |
| 26 |  38 | & |
| 27 |  39 | ' |
| 28 |  40 | ( |
| 29 |  41 | ) |
| 2a |  42 | * |
| 2b |  43 | + |
| 2c |  44 | , |
| 2d |  45 | - |
| 2e |  46 | . |
| 2f |  47 | / |
| 30 |  48 | 0 |
| 31 |  49 | 1 |
| 32 |  50 | 2 |
| 33 |  51 | 3 |
| 34 |  52 | 4 |
| 35 |  53 | 5 |
| 36 |  54 | 6 |
| 37 |  55 | 7 |
| 38 |  56 | 8 |
| 39 |  57 | 9 |
| 3a |  58 | : |
| 3b |  59 | ; |
| 3c |  60 | < |
| 3d |  61 | = |
| 3e |  62 | > |
| 3f |  63 | ? |
| 40 |  64 | @ |
| 41 |  65 | A |
| 42 |  66 | B |
| 43 |  67 | C |
| 44 |  68 | D |
| 45 |  69 | E |
| 46 |  70 | F |
| 47 |  71 | G |
| 48 |  72 | H |
| 49 |  73 | I |
| 4a |  74 | J |
| 4b |  75 | K |
| 4c |  76 | L |
| 4d |  77 | M |
| 4e |  78 | N |
| 4f |  79 | O |
| 50 |  80 | P |
| 51 |  81 | Q |
| 52 |  82 | R |
| 53 |  83 | S |
| 54 |  84 | T |
| 55 |  85 | U |
| 56 |  86 | V |
| 57 |  87 | W |
| 58 |  88 | X |
| 59 |  89 | Y |
| 5a |  90 | Z |
| 5b |  91 | [ |
| 5c |  92 | \ |
| 5d |  93 | ] |
| 5e |  94 | ^ |
| 5f |  95 | _ |
| 60 |  96 | ` |
| 61 |  97 | a |
| 62 |  98 | b |
| 63 |  99 | c |
| 64 | 100 | d |
| 65 | 101 | e |
| 66 | 102 | f |
| 67 | 103 | g |
| 68 | 104 | h |
| 69 | 105 | i |
| 6a | 106 | j |
| 6b | 107 | k |
| 6c | 108 | l |
| 6d | 109 | m |
| 6e | 110 | n |
| 6f | 111 | o |
| 70 | 112 | p |
| 71 | 113 | q |
| 72 | 114 | r |
| 73 | 115 | s |
| 74 | 116 | t |
| 75 | 117 | u |
| 76 | 118 | v |
| 77 | 119 | w |
| 78 | 120 | x |
| 79 | 121 | y |
| 7a | 122 | z |
| 7b | 123 | { |
| 7c | 124 | | |
| 7d | 125 | } |
| 7e | 126 | ~ |
```

From the above, we can not print `128`, and below is a LOCALE table,

<table>
<tbody><tr><td><tt>0020 — 007F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0020-007F">Basic Latin</a></td><td>&nbsp;</td><td><tt>2580 — 259F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2580-259F">Block Elements</a></td></tr>
<tr><td><tt>00A0 — 00FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/00A0-00FF">Latin-1 Supplement</a></td><td>&nbsp;</td><td><tt>25A0 — 25FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/25A0-25FF">Geometric Shapes</a></td></tr>
<tr><td><tt>0100 — 017F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0100-017F">Latin Extended-A</a></td><td>&nbsp;</td><td><tt>2600 — 26FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2600-26FF">Miscellaneous Symbols</a></td></tr>
<tr><td><tt>0180 — 024F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0180-024F">Latin Extended-B</a></td><td>&nbsp;</td><td><tt>2700 — 27BF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2700-27BF">Dingbats</a></td></tr>
<tr><td><tt>0250 — 02AF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0250-02AF">IPA Extensions</a></td><td>&nbsp;</td><td><tt>27C0 — 27EF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/27C0-27EF">Miscellaneous Mathematical Symbols-A</a></td></tr>
<tr><td><tt>02B0 — 02FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/02B0-02FF">Spacing Modifier Letters</a></td><td>&nbsp;</td><td><tt>27F0 — 27FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/27F0-27FF">Supplemental Arrows-A</a></td></tr>
<tr><td><tt>0300 — 036F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0300-036F">Combining Diacritical Marks</a></td><td>&nbsp;</td><td><tt>2800 — 28FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2800-28FF">Braille Patterns</a></td></tr>
<tr><td><tt>0370 — 03FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0370-03FF">Greek and Coptic</a></td><td>&nbsp;</td><td><tt>2900 — 297F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2900-297F">Supplemental Arrows-B</a></td></tr>
<tr><td><tt>0400 — 04FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0400-04FF">Cyrillic</a></td><td>&nbsp;</td><td><tt>2980 — 29FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2980-29FF">Miscellaneous Mathematical Symbols-B</a></td></tr>
<tr><td><tt>0500 — 052F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0500-052F">Cyrillic Supplementary</a></td><td>&nbsp;</td><td><tt>2A00 — 2AFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2A00-2AFF">Supplemental Mathematical Operators</a></td></tr>
<tr><td><tt>0530 — 058F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0530-058F">Armenian</a></td><td>&nbsp;</td><td><tt>2B00 — 2BFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2B00-2BFF">Miscellaneous Symbols and Arrows</a></td></tr>
<tr><td><tt>0590 — 05FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0590-05FF">Hebrew</a></td><td>&nbsp;</td><td><tt>2E80 — 2EFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2E80-2EFF">CJK Radicals Supplement</a></td></tr>
<tr><td><tt>0600 — 06FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0600-06FF">Arabic</a></td><td>&nbsp;</td><td><tt>2F00 — 2FDF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2F00-2FDF">Kangxi Radicals</a></td></tr>
<tr><td><tt>0700 — 074F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0700-074F">Syriac</a></td><td>&nbsp;</td><td><tt>2FF0 — 2FFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2FF0-2FFF">Ideographic Description Characters</a></td></tr>
<tr><td><tt>0780 — 07BF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0780-07BF">Thaana</a></td><td>&nbsp;</td><td><tt>3000 — 303F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3000-303F">CJK Symbols and Punctuation</a></td></tr>
<tr><td><tt>0900 — 097F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0900-097F">Devanagari</a></td><td>&nbsp;</td><td><tt>3040 — 309F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3040-309F">Hiragana</a></td></tr>
<tr><td><tt>0980 — 09FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0980-09FF">Bengali</a></td><td>&nbsp;</td><td><tt>30A0 — 30FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/30A0-30FF">Katakana</a></td></tr>
<tr><td><tt>0A00 — 0A7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0A00-0A7F">Gurmukhi</a></td><td>&nbsp;</td><td><tt>3100 — 312F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3100-312F">Bopomofo</a></td></tr>
<tr><td><tt>0A80 — 0AFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0A80-0AFF">Gujarati</a></td><td>&nbsp;</td><td><tt>3130 — 318F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3130-318F">Hangul Compatibility Jamo</a></td></tr>
<tr><td><tt>0B00 — 0B7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0B00-0B7F">Oriya</a></td><td>&nbsp;</td><td><tt>3190 — 319F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3190-319F">Kanbun</a></td></tr>
<tr><td><tt>0B80 — 0BFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0B80-0BFF">Tamil</a></td><td>&nbsp;</td><td><tt>31A0 — 31BF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/31A0-31BF">Bopomofo Extended</a></td></tr>
<tr><td><tt>0C00 — 0C7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0C00-0C7F">Telugu</a></td><td>&nbsp;</td><td><tt>31F0 — 31FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/31F0-31FF">Katakana Phonetic Extensions</a></td></tr>
<tr><td><tt>0C80 — 0CFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0C80-0CFF">Kannada</a></td><td>&nbsp;</td><td><tt>3200 — 32FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3200-32FF">Enclosed CJK Letters and Months</a></td></tr>
<tr><td><tt>0D00 — 0D7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0D00-0D7F">Malayalam</a></td><td>&nbsp;</td><td><tt>3300 — 33FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3300-33FF">CJK Compatibility</a></td></tr>
<tr><td><tt>0D80 — 0DFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0D80-0DFF">Sinhala</a></td><td>&nbsp;</td><td><tt>3400 — 4DBF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/3400-4DBF">CJK Unified Ideographs Extension A</a></td></tr>
<tr><td><tt>0E00 — 0E7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0E00-0E7F">Thai</a></td><td>&nbsp;</td><td><tt>4DC0 — 4DFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/4DC0-4DFF">Yijing Hexagram Symbols</a></td></tr>
<tr><td><tt>0E80 — 0EFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0E80-0EFF">Lao</a></td><td>&nbsp;</td><td><tt>4E00 — 9FFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/4E00-9FFF">CJK Unified Ideographs</a></td></tr>
<tr><td><tt>0F00 — 0FFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/0F00-0FFF">Tibetan</a></td><td>&nbsp;</td><td><tt>A000 — A48F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/A000-A48F">Yi Syllables</a></td></tr>
<tr><td><tt>1000 — 109F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1000-109F">Myanmar</a></td><td>&nbsp;</td><td><tt>A490 — A4CF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/A490-A4CF">Yi Radicals</a></td></tr>
<tr><td><tt>10A0 — 10FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10A0-10FF">Georgian</a></td><td>&nbsp;</td><td><tt>AC00 — D7AF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/AC00-D7AF">Hangul Syllables</a></td></tr>
<tr><td><tt>1100 — 11FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1100-11FF">Hangul Jamo</a></td><td>&nbsp;</td><td><tt>D800 — DB7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/D800-DB7F">High Surrogates</a></td></tr>
<tr><td><tt>1200 — 137F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1200-137F">Ethiopic</a></td><td>&nbsp;</td><td><tt>DB80 — DBFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/DB80-DBFF">High Private Use Surrogates</a></td></tr>
<tr><td><tt>13A0 — 13FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/13A0-13FF">Cherokee</a></td><td>&nbsp;</td><td><tt>DC00 — DFFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/DC00-DFFF">Low Surrogates</a></td></tr>
<tr><td><tt>1400 — 167F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1400-167F">Unified Canadian Aboriginal Syllabics</a></td><td>&nbsp;</td><td><tt>E000 — F8FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/E000-F8FF">Private Use Area</a></td></tr>
<tr><td><tt>1680 — 169F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1680-169F">Ogham</a></td><td>&nbsp;</td><td><tt>F900 — FAFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/F900-FAFF">CJK Compatibility Ideographs</a></td></tr>
<tr><td><tt>16A0 — 16FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/16A0-16FF">Runic</a></td><td>&nbsp;</td><td><tt>FB00 — FB4F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FB00-FB4F">Alphabetic Presentation Forms</a></td></tr>
<tr><td><tt>1700 — 171F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1700-171F">Tagalog</a></td><td>&nbsp;</td><td><tt>FB50 — FDFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FB50-FDFF">Arabic Presentation Forms-A</a></td></tr>
<tr><td><tt>1720 — 173F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1720-173F">Hanunoo</a></td><td>&nbsp;</td><td><tt>FE00 — FE0F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FE00-FE0F">Variation Selectors</a></td></tr>
<tr><td><tt>1740 — 175F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1740-175F">Buhid</a></td><td>&nbsp;</td><td><tt>FE20 — FE2F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FE20-FE2F">Combining Half Marks</a></td></tr>
<tr><td><tt>1760 — 177F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1760-177F">Tagbanwa</a></td><td>&nbsp;</td><td><tt>FE30 — FE4F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FE30-FE4F">CJK Compatibility Forms</a></td></tr>
<tr><td><tt>1780 — 17FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1780-17FF">Khmer</a></td><td>&nbsp;</td><td><tt>FE50 — FE6F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FE50-FE6F">Small Form Variants</a></td></tr>
<tr><td><tt>1800 — 18AF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1800-18AF">Mongolian</a></td><td>&nbsp;</td><td><tt>FE70 — FEFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FE70-FEFF">Arabic Presentation Forms-B</a></td></tr>
<tr><td><tt>1900 — 194F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1900-194F">Limbu</a></td><td>&nbsp;</td><td><tt>FF00 — FFEF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FF00-FFEF">Halfwidth and Fullwidth Forms</a></td></tr>
<tr><td><tt>1950 — 197F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1950-197F">Tai Le</a></td><td>&nbsp;</td><td><tt>FFF0 — FFFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/FFF0-FFFF">Specials</a></td></tr>
<tr><td><tt>19E0 — 19FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/19E0-19FF">Khmer Symbols</a></td><td>&nbsp;</td><td><tt>10000 — 1007F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10000-1007F">Linear B Syllabary</a></td></tr>
<tr><td><tt>1D00 — 1D7F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1D00-1D7F">Phonetic Extensions</a></td><td>&nbsp;</td><td><tt>10080 — 100FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10080-100FF">Linear B Ideograms</a></td></tr>
<tr><td><tt>1E00 — 1EFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1E00-1EFF">Latin Extended Additional</a></td><td>&nbsp;</td><td><tt>10100 — 1013F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10100-1013F">Aegean Numbers</a></td></tr>
<tr><td><tt>1F00 — 1FFF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1F00-1FFF">Greek Extended</a></td><td>&nbsp;</td><td><tt>10300 — 1032F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10300-1032F">Old Italic</a></td></tr>
<tr><td><tt>2000 — 206F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2000-206F">General Punctuation</a></td><td>&nbsp;</td><td><tt>10330 — 1034F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10330-1034F">Gothic</a></td></tr>
<tr><td><tt>2070 — 209F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2070-209F">Superscripts and Subscripts</a></td><td>&nbsp;</td><td><tt>10380 — 1039F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10380-1039F">Ugaritic</a></td></tr>
<tr><td><tt>20A0 — 20CF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/20A0-20CF">Currency Symbols</a></td><td>&nbsp;</td><td><tt>10400 — 1044F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10400-1044F">Deseret</a></td></tr>
<tr><td><tt>20D0 — 20FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/20D0-20FF">Combining Diacritical Marks for Symbols</a></td><td>&nbsp;</td><td><tt>10450 — 1047F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10450-1047F">Shavian</a></td></tr>
<tr><td><tt>2100 — 214F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2100-214F">Letterlike Symbols</a></td><td>&nbsp;</td><td><tt>10480 — 104AF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10480-104AF">Osmanya</a></td></tr>
<tr><td><tt>2150 — 218F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2150-218F">Number Forms</a></td><td>&nbsp;</td><td><tt>10800 — 1083F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/10800-1083F">Cypriot Syllabary</a></td></tr>
<tr><td><tt>2190 — 21FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2190-21FF">Arrows</a></td><td>&nbsp;</td><td><tt>1D000 — 1D0FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1D000-1D0FF">Byzantine Musical Symbols</a></td></tr>
<tr><td><tt>2200 — 22FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2200-22FF">Mathematical Operators</a></td><td>&nbsp;</td><td><tt>1D100 — 1D1FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1D100-1D1FF">Musical Symbols</a></td></tr>
<tr><td><tt>2300 — 23FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2300-23FF">Miscellaneous Technical</a></td><td>&nbsp;</td><td><tt>1D300 — 1D35F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1D300-1D35F">Tai Xuan Jing Symbols</a></td></tr>
<tr><td><tt>2400 — 243F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2400-243F">Control Pictures</a></td><td>&nbsp;</td><td><tt>1D400 — 1D7FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/1D400-1D7FF">Mathematical Alphanumeric Symbols</a></td></tr>
<tr><td><tt>2440 — 245F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2440-245F">Optical Character Recognition</a></td><td>&nbsp;</td><td><tt>20000 — 2A6DF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/20000-2A6DF">CJK Unified Ideographs Extension B</a></td></tr>
<tr><td><tt>2460 — 24FF</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2460-24FF">Enclosed Alphanumerics</a></td><td>&nbsp;</td><td><tt>2F800 — 2FA1F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2F800-2FA1F">CJK Compatibility Ideographs Supplement</a></td></tr>
<tr><td><tt>2500 — 257F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/2500-257F">Box Drawing</a></td><td>&nbsp;</td><td><tt>E0000 — E007F</tt>&nbsp;&nbsp;</td><td><a href="/r/Unicode/E0000-E007F">Tags</a></td></tr>
</tbody></table>

So we may want just print `128` in [UTF-8](https://www.compart.com/en/unicode/U+20AC), namely `U+20AC`
```
# cat h.c
#include <stdio.h>

int main() {
        printf("%s\n", "\u20AC");

}
# ./a.out 
€
```

### Print Styles

Here we want to show different ways of print out latin word `ý`, which is *Latin small letter y with acute*.

1. ASCII Extend
```
$ cat a.c
#include <stdio.h>

int main()
{
        printf("%d => %c\n", 253, 253);
        return 0;
}

$ gcc a.c
$ ./a.out
253 => �
```
2. UTF-16 (hex)
```
#include <stdio.h>
#include <wchar.h>
#include <locale.h>

int main() {
    setlocale(LC_CTYPE, "");
    wchar_t star = 0x00FD;;
    wprintf(L"%lc\n", star);
}
```
3. UTF-8 (hex)
```
#include <stdio.h>

int main() {
        printf("%c%c\n", '\xC3', '\xBD');

}
```
4. UTF-16 (unicode)
```
#include <stdio.h>

int main() {
        printf("%s\n", "\u00FD");

}
```

### Bagua
```
#include <stdio.h>
#include <locale.h>

#ifndef __STDC_ISO_10646__
#error "Oops, our wide chars are not Unicode codepoints, sorry!"
#endif
int main()
{
        int i;
        setlocale(LC_ALL, "");
        printf("__________________\n");
        for (i = 0x4DC0; i < 0x4DC0 + 64; i++) {
                printf("| %2d | %lc | %04x |\n", i - 0x4DC0 + 1, i, i - 0x4DC0);
        }
        printf("------------------\n");
        return 0;
}
```

<a href="#top">Back to top</a>
