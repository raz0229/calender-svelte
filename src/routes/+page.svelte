<script>
 const month = ['January', 'Febuary', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'];
 //const week_days = ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat'];
 const week_days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
 const days = [28 || 29, 30, 31];
 const date = new Date();
 const year = date.getFullYear();
 let doomsDay = [3, 28, 14, 4, 9, 6, 11, 8, 5, 10, 7, 12];
 const PIday = new Date(`March 14, ${year}`);
 const dayOfDoom = PIday.getDay();
 let monLen = []
 let firstDay = []
 let monCal = [[],[],[],[],[],[],[],[],[],[],[],[],]
 let yearObj = {}

 
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
 }
 getDay(doomsDay, dayOfDoom)


 function arr42() {
     for (let i = 0; i < month.length; i++) {
	 let k = monLen.at(i -1 );
         for (let j = firstDay[i]; j > 0; j--) {
             monCal[i].unshift(k);
	     k--
         }
         for (let j = 1; j <= monLen[i]; j++) {
             monCal[i].push(j);
         }
	 k = 1
	 for (let j = monCal[i].length; j < 42; j++) {
             monCal[i].push(k);
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
	     temp.push(monCal[i].slice(start, j))
	     start +=7
	 }
	 monCal[i] = temp
     }
 }
 arrSplit()

 function objMaker(x, y, z){
     y.forEach((e, i) => {
	 x[e] = z[i];
     });    
 }
 objMaker(yearObj, month, monCal)
 console.log(yearObj.length)


 function 3rdYear(){
     let main = `<div class=' bg-black grid lg:grid-cols-2 place-content-evenly gap-12 m-12 '>
    {#each Object.entries(yearObj) as [key, value], index (key)}
	{#if index > 7}
	    <div class="inline-block bg-slate-900 flex flex-col flex-nowrap items-center p-0 border break-after-page">
		
	<p class="block text-center py-1.5 ">{key}</p>
	<table class=" bg-slate-500 bg-opacity-50 w-full">
	    <thead>
		<tr class="daysWeek">
		    {#each week_days as col}
			
			{#if col == 'Sunday' || col == 'Saturday'}
			    <th class="text-purple-900 border border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{:else}
			    <th class="text-black border border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{/if}
		    {/each}
		</tr>
	    </thead>
	    <tbody>
		{#each value as mon}
		    
	    <tr class="daysMon">
		{#each mon as cell}
		    
		    <td class="border border-gray-900 py-1.5">{cell}</td>
		{/each}
	    </tr>
		{/each}
	    </tbody>
	</table>
	</div>`
 }
</script>


<body class="bg-black">
<h1 class="text-white text-2xl text-center pt-6">Welcome to {year}</h1>
<div class=' bg-black grid lg:grid-cols-2 place-content-evenly gap-12 m-12 '>
    {#each Object.entries(yearObj) as [key, value], index (key)}
	{#if index > 7}
	    <div class="inline-block bg-slate-900 flex flex-col flex-nowrap items-center p-0 border break-after-page">
		
	<p class="block text-center py-1.5 ">{key}</p>
	<table class=" bg-slate-500 bg-opacity-50 w-full">
	    <thead>
		<tr class="daysWeek">
		    {#each week_days as col}
			
			{#if col == 'Sunday' || col == 'Saturday'}
			    <th class="text-purple-900 border border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{:else}
			    <th class="text-black border border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{/if}
		    {/each}
		</tr>
	    </thead>
	    <tbody>
		{#each value as mon}
		    
	    <tr class="daysMon">
		{#each mon as cell}
		    
		    <td class="border border-gray-900 py-1.5">{cell}</td>
		{/each}
	    </tr>
		{/each}
	    </tbody>
	</table>
	</div>
    {:else if index > 3}
 	<div class="inline-block bg-slate-500 flex flex-col flex-nowrap items-center p-0 border">
	<p class="block text-center py-1.5 ">{key}</p>
	<table class=" bg-slate-500 bg-opacity-50 w-full">
	    <thead>
		<tr class="daysWeek">
		    {#each week_days as col}
			
			{#if col == 'Sunday' || col == 'Saturday'}
			    <th class="text-purple-900 border rounded-lg border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{:else}
			    <th class="text-black border rounded-lg border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{/if}
		    {/each}
		</tr>
	    </thead>
	    <tbody>
		{#each value as mon}
		    
	    <tr class="daysMon">
		{#each mon as cell}
		    
		    <td class="border roudend border-gray-900 py-1.5">{cell}</td>
		{/each}
	    </tr>
		{/each}
	    </tbody>
	</table>
	</div>
{:else}
	<div class="inline-block bg-slate-500 flex flex-col flex-nowrap items-center p-0 border break-after-page">
	<p class="block text-center py-1.5 ">{key}</p>
	<table class=" bg-slate-500 bg-opacity-50 w-full">
	    <thead>
		<tr class="daysWeek">
		    {#each week_days as col}
			
			{#if col == 'Sunday' || col == 'Saturday'}
			    <th class="text-purple-900 border rounded-lg border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{:else}
			    <th class="text-black border rounded-lg border-gray-900 shrink px-2.5 py-1.5">{col}</th>
			{/if}
		    {/each}
		</tr>
	    </thead>
	    <tbody>
		{#each value as mon}
		    
	    <tr class="daysMon">
		{#each mon as cell}
		    
		    <td class="border roudend border-gray-900 py-1.5">{cell}</td>
		{/each}
	    </tr>
		{/each}
	    </tbody>
	</table>
	</div>
{/if}

{/each}
<footer class ="bg-black">
    
</footer>
</body>

