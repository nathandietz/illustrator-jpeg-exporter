# A breakdown of the Export JPEG Illustrator Action 


### Image Quality
```
imagQual = "06000000"; /*  Range: 0-10
                          01000000 = Low
                          03000000 = Medium
                          06000000 = High
                          08000000 = Maximum
                      */
```

// Compression Method
```
compMeth = "01000000"; /*  Range: 1-3
                          01000000 = Baseline (Standard)
                          02000000 = Baseline Optimzied
                          03000000 = Progressive 
                      */
// Number of Scans
numScans = "03000000"; /*  Range: 3-5
                          03000000 = 3 Scans
                          04000000 = 4 Scans
                          05000000 = 5 Scans

                          This is only applicable when using Progressive compression "03000000"
                      */
// Anti-aliasing
aliasing = "02000000" /*  Range: 1-3
                          01000000 = None
                          02000000 = Art Optimzied  (Supersampling)
                          03000000 = Type Optimzied (Hinted)
                      */                               
// Image Resolution
imageRes = "00002c01" /*  00004800 = Screen (72 dpi)
                          00009600 = Medium (150 dpi)
                          00002c01 = High   (300 dpi)
                          00005802 = Max    (600 dpi)
                      */
// Color Model
colorMdl = "02000000"; /*  Range: 1-3
                          01000000 = RGB
                          02000000 = CMYK
                          03000000 = Grayscale 
                      */                                
// Image Map
imageMap = "02000000"; /*  Range: 2-3
                          02000000 = Disabled
                          03000000 = Enabled 
                      */ 
// Image Map Style
mapStyle = "02000000"; /*  Range: 1-2
                          01000000 = Client (.html)
                          02000000 = Server (.map)
                      */                                             
// ICC Profile
iccProfl = "00000100"; /*  Range: 0-1
                          00000000 = Do not embed ICC Profile
                          00000100 = Embed ICC Profile
                      */

```
##### Warning: The code below will not run because of the comments
Illustrator actions are very unforgiving and will throw an error unless the formating is perfect. For a working version, reference the .jsx script.

-------------

##### Unicode Strings & Hex Strings
Illustrator actions convert most unicode strings to hex strings. You can use [onlinehextools.com/convert-hex-to-string](https://onlinehextools.com/convert-hex-to-string) (or something similar) to convert from `string <=> hex`.

```
/version 3
	/* Name of Illustrator Set: set1 */
	/name [ 4       	// 01 | 02 | 03 | 04	Number of characters in string	
		73657431	// 73 | 65 | 74 | 31	Hexadecimal string                         
	]               	// s  | e  | t  | 1	Unicode string
	/isOpen        0    
	/actionCount   1  
	
	/action-1 {
		/* Name of Illustrtor Action: act1 */
		/name [ 4       	// 01 | 02 | 03 | 04	Number of characters in string
			61637431	// 61 | 63 | 74 | 31	Hexadecimal string
		]               	// a  | c  | t  | 1	Unicode string
		
		/keyIndex    1
		/colorIndex  0
		/isOpen      1
		/eventCount  1

		/event-1 {
			/useRulersIn1stQuadrant 0
			/internalName (adobe_exportDocument)
			/localizedName [ 9        	// 01 | 02 | 03 | 04 | 05 | 06 | 07 | 08 | 09
				4578706f7274204173	// 45 | 78 | 70 | 6f | 72 | 74 | 20 | 41 | 73         
			]                         	// E  | x  | p  | o  | r  | t  |    | A  | s

			/isOpen          0
			/isOn            1
			/hasDialog       1
			/showDialog      0
			/parameterCount  7         	// Number of 'Export As' settings

			/** Defines: export settings **/
			/parameter-1 {
				/key 1885434477		 
				/showInPalette 0
				/type (raw)/value < 100
				     /* imagQual = Image Quality
					compMeth = Compression Method
					numScans = Number of Scan (Only applicable with Progressive Compression)
					aliasing = Anti-Aliasing
					imageRes = Image Resolution
					colorMdl = Color Model
					imageMap = Image Map
					mapStyle = Image Map Style
					iccProfl = ICC Profile */

				     /* imagQual   compMeth   numScans   aliasing   imageRes   colorMdl   imageMap   mapStyle */
					06000000   01000000   03000000   02000000   00002c01   02000000   02000000   02000000   // Each of 8 charater group repersents the individual export settings.

				     /* i � m �	   a � g �    e � m �    a � p � */
					69006d00   61006700   65006d00   61007000   00000000   00000000   00000000   00000000   // Uknown: The first 32 charactes spellout: i�m�a�g�e�m�a�p�
					00000000   00000000   00000000   00000000   00000000   00000000   00000000   00000000   // Uknown: Padding perhaps?

				     /* iccProfl */
					00000100																				
				>
				/size 100
			}

			/** Defines: file path for file export **/
			/parameter-2 {
				/key 1851878757
				/showInPalette 4294967295			
				/type (ustring)
				/value [ 19 					// Number of characters in file export path
					2f706174682f746f2f6578706f72742e6a7067	// /path/to/export.jpg
				]
			}

			/** Defines: image file format **/
			/parameter-3 {
				/key 1718775156
				/showInPalette 4294967295
				/type (ustring)
				/value [ 16 					// Number of characters in file format string
					4a5045472066696c6520666f726d6174	// JPEG file format
				]
			}

			/** Defines: file extention **/
			/parameter-4 {
				/key 1702392942
				/showInPalette 4294967295
				/type (ustring)
				/value [ 12 					// Number of characters in file extention string
					6a70672c6a70652c6a706567		// jpg,jpe,jpeg
				]
			}

			/** Defines: 'Use Artboards' Checkbox **/
			/parameter-5 {
				/key 1936548194
				/showInPalette 4294967295
				/type (boolean)
				/value 1		// 1 = checked | 0 = unchecked
			}				// If '0' is set (unchecked) then both parameter-6 & parameter-7 are ignored

			/** Defines: 'All' or 'Range' Radio Button **/
			/parameter-6 {
				/key 1935764588
				/showInPalette 4294967295
				/type (boolean)
				/value 0		// 1 = All, 0 = Range
			}				// If '1' is set then parameter-7 is ignored

			/** Defines: Range of Artbords to Export */
			/parameter-7 {
				/key 1936875886
				/showInPalette 4294967295
				/type (ustring)
				/value [ 0]		// [ 0] = All, [ 1 31] = Artboard #1 , [ 1 32] = Artboard #2, et cetera
			}
		}
	}
```