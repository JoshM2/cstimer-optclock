# Please read this!

Note: this does not work with cstimer+.
After installing this extension, open up the tools selector and choose optclock. The optimal movecount will now be displayed when you hit next scramble. It is important to note that you won't be able to click any buttons while the optimal solution is being generated, so don't try to spam the next scramble button when optclock is your selected tool.

To install this extension on chrome:
1) go to chrome://extensions/
2) turn on developer mode
3) click load unpacked
4) select the folder where you downloaded this

The way this works is that it runs optclock compiled to webassembly. Webassembly code can't be read, so technically I could be running something malicious (I'm not). If you want the peace of mind, I'll write how to compile the modifiedoptclock.cpp file to webassembly below.

steps if you want to compile it to webassembly yourself:
1) Delete the optclock.wasm file
2) Install emscripten - https://emscripten.org/docs/getting_started/downloads.html
3) Run the following command:
em++ modifiedoptclock.cpp -O3 -o optclock.js -s EXPORT_ALL=1
4) You should now have a optclock.wasm and optclock.js file. If they aren't in the folder of the extension move them there.
5) open up the optclock.js file and copy everything inside.
6) Open up the content.js file, and delete everything inside of the fetchOutput function. Now paste what you have copied from the optclock.js file.
7) You can now delete the optclock.js file if you'd like.
8) ctrl F through the contents.js file to find "optclock.wasm" inside the code you just pasted. Replace this with:
chrome.runtime.getURL("optclock.wasm")
9) Now ctrl F again to find "prompt". Replace result=window.prompt("Input: ") with:
result = scramble
10) It should work now. Let me know on discord if it doesn't and I'll be happy to help.
