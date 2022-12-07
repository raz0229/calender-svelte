<script>
 const month = ['January', 'Febuary', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
 const week_days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
 const days = [28 || 29, 30, 31];
 const date = new Date();
 const year = date.getFullYear();
 let doomsDay = [3, 28, 14, 4, 9, 6, 11, 8, 5, 10, 7, 12];
 const PIday = new Date(`March 14, ${year}`);
 const dayOfDoom = PIday.getDay();
 let monLen = []
 let firstDay = []

 function calcLeap(x) {
     if (x % 4 == 0) {
         const leap = true;
         days[0] = 29;
         doomsDay[0] += 1;
         doomsDay[1] += 1;
     }
     else {
         const leap = false;
         days[0] = 28;
     }
 }
 calcLeap(year);

 function daysInMon(x, y) {
     for (let i = 0; i <= 11; i++) {
         if (i == 1) {
             monLen.push(y[0]);
         }
         if (i == 3 || i == 5 || i == 8 || i == 10) {
             monLen.push(y[1]);
         }
         else {
             monLen.push(y[2]);
         }
     }
     console.log(monLen)
 }
 daysInMon(month, days);

 function getDay(x, y) {
     for (let i = 0; i < x.length; i++) {
	 let ans = x[i] % 7 - (y+1)
	 if(ans > 0) {
	     firstDay.push(7 - ans)	    
	 }
	 else {
	     firstDay.push(-ans)
	 }
     }
     console.log(firstDay)
 }
 getDay(doomsDay, dayOfDoom)


 function arr42() {
     for (let i = 0; i < month.length; i++) {
         this[month[i] + 'Arr'] = new Array();
	 let k = monLen.at(i -1 );
         for (let j = firstDay[i]; j > 0; j--) {
             this[month[i] + 'Arr'].unshift(k);
	     k--
         }
         for (let j = 1; j <= monLen[i]; j++) {
             this[month[i] + 'Arr'].push(j);
         }
	 k = 1
	 for (let j = this[month[i] + 'Arr'].length; j < 42; j++) {
             this[month[i] + 'Arr'].push(k);
	     k++
         }
     }
 }
 arr42()

 function arrSplit() {
     for (let i = 0; i < month.length; i++) {
	 let temp = []
	 let start = 0
	 for(let j = 7; j < 43; j += 7) {
	     temp.push(this[month[i] + 'Arr'].slice(start, j))
	     start +=7
	 }
	 this[month[i] + 'Arr'] = temp
     }
 }
 arrSplit()
 console.table(MayArr)
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
