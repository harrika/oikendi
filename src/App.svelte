<script>
	let city = null;
	let cntry = ""
	let weatherloc = "";
	let weatherdesc2 = "";
	let weatherwind = "";
	let weathertemp = null;
	$: tempc = (weathertemp - 273.15).toFixed(2);; 
	$: tempfar = ((tempc*9/5)+32).toFixed(2);	
	
function kendi() {
	// city = mm;
	fetch(`http://api.openweathermap.org/data/2.5/weather?q=${city}&APPID=a98fa2f15f9189fb40a7332d4855fa41`, {mode: 'cors'})
	      .then(function(response){
	        return response.json()
	      })
	      .then((response) => {
	        weatherloc = response.name;
	        cntry = response.sys.country;
	        weathertemp = response.main.temp;
	        weatherdesc2 = response.weather[0].description;
	        weatherwind = response.wind.speed;
	        console.log(response);
	      })
 }

</script>

<style>
	.mt {
		margin-top: 20px;
	}
	.mb {
		margin-bottom: 20px;
	}
	.lm {
		margin-left: 20px;
	}
</style>
	<section class="hero is-primary mt mb">
	  <div class="hero-body">
	    <div class="container">
	      <h1 class="title">
	        svelther
	      </h1>
	      <h2 class="subtitle">
	        Know you weather!
	      </h2>
	    </div>
	  </div>
	</section>

<div class="container">
	<div class="columns">
		<div class="column is-4">
				<div class="form">
			 	<div class="field">
				<label for="" class="label">
				<i class="fas fa-cloud-rain" style="color:hsl(141, 71%, 71%)"></i> Enter a city name</label>
			   <span>
			   <input class="input" type="text" placeholder="city: London,uk" bind:value={city}>			   	
			   </span>

				</div> <!-- end field -->

				<div class="field">
					<p class="control">
					<button class="button is-info" on:click={()=>kendi()}>
					check weather</button>			
					</p>
				</div>		
				</div><!--  end form -->			
		</div> <!-- end col1 -->

		<div class="column is-8">
		<table class="table is-narrow is-hoverable is-striped lm" style="width:50%">		
			<tbody>
				<tr>
				  <td>location: </td> 
				  <td>{weatherloc} {cntry}</td>
				</tr>			  
				<tr>
				  <td>wind speed</td>
				  <td>{weatherwind}</td>
				</tr>			  
				<tr>
				  <td>temperatures:</td>
				  <td>{tempc} oC, {tempfar} oF</td>
				</tr>			  
				<tr>
				  <td>weather: </td>
				  <td>{weatherdesc2}</td>
				</tr>			  				
			</tbody>			  
		</table>
		</div> <!-- end col2 -->
	</div>	<!-- end cols -->
	
</div> <!-- end container -->
