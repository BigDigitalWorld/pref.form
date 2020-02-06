# pref.form
Preference Form - Bootstrap 4

<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Form</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
  <script src="https://ajax.aspnetcdn.com/ajax/jquery.validate/1.14.0/jquery.validate.min.js"></script>
  <script src="https://ajax.aspnetcdn.com/ajax/jquery.validate/1.14.0/additional-methods.js"></script>
</head>
<body>

 <script>
 
    $(document).ready(function(){
			    (function($){
                    $.getQuery = function( query ) {
                        query = query.replace(/[\[]/,"\\\[").replace(/[\]]/,"\\\]");
                        var expr = "[\\?&]"+query+"=([^&#]*)";
                        var regex = new RegExp( expr );
                        var results = regex.exec( window.location.href );
                        if( results !== null ) {
                            return results[1];
                            return decodeURIComponent(results[1].replace(/\+/g, " "));
                        } 
                        else {
                            return false;
                        }
                    };
                })(jQuery);
                
                var divHtml, p = $.getQuery('p');

                switch (p) { 
					case 'option1': 
						divHtml = $('#id1').html();
					    $('#id1').remove();
					    $('#id2').prepend(divHtml);
						break;
					case 'option2': 
						divHtml = $('#id2').html();
					    $('#id2').remove();
					    $('#prefContainer').prepend(divHtml);
						break;
					case 'option3': case 'option4':
						divHtml = $('#id3').html();
					    $('#id3').remove();
					    $('#prefContainer').prepend(divHtml);
						break;
					
					default:
						break;
				}

				$("#mailingstate").val($("#s_mailingstate").val());
		        $("#mailingcountrycode").val($("#s_mailingcountrycode").val());

				$("#option1").prop('checked' ,( $("#s_option1").val()=='100' ? true : false ) );
        		$("#option2").prop('checked' ,( $("#s_option2").val()=='100' ? true : false ) );
        		$("#option3").prop('checked' ,( $("#s_option3").val()=='100' ? true : false ) );
        		$("#option4").prop('checked' ,( $("#s_option4").val()=='100' ? true : false ) );
        		

				var dob = $("#dob").val();
				if (dob != '' && dob !== undefined){
					$("#year").val($("#s_dob").val().substring(0, 4));
		            $("#month").val($("#s_dob").val().substring(5, 7));
		            $("#day").val($("#s_dob").val().substring(8, 10));
				}
				
                $("#signin").click(function(e){
                	var validator = $( "#registerForm" ).validate();
					if (validator.form()){
	                	e.preventDefault();

	                	var min_age = 13;
		            	var year = $("#year").val();
		            	var month = $("#month").val();
		            	var day = $("#day").val();
		            	
		            	if (month != '' || day != '' || year != ''){
							if (month == '' || day == '' || year == ''){
								$("#bdayerror").html("Please fill in all values.");
				            	return false;
							}
							else{		            		
				            	var theirDate = new Date((parseInt(year) + parseInt(min_age)), (month -1), day);
				            	var today = new Date;
				            	
				            	if (  (today.getTime() - theirDate.getTime()) < 0) {
				            		$("#bdayerror").html("You need to be at least 13 to enter.");
				            		return false;
				            	}
				            	else{
				            		$("#s_dob").val($("#month").val()+"/"+$("#day").val()+"/"+$("#year").val());
				            		$("#s_email").val($("#s_email_string").val());
				            		$("#s_mailingstate").val($("#mailingstate").val());
				            		$("#s_mailingcountrycode").val($("#mailingcountrycode").val());
				            		$("#s_option1").val( $("#id1").is(':checked') ? '100' : '1500' );
				            		$("#s_option2").val( $("#id2").is(':checked') ? '100' : '1500' );
				            		$("#s_option3").val( $("#id3").is(':checked') ? '100' : '1500' );
				            		
				            		$("#registerForm").submit();
				            	}
				            }
			            }
		            	else {
		            		$("#s_email").val($("#s_email_string").val());
		            		$("#s_mailingstate").val($("#mailingstate").val());
		            		$("#s_mailingcountrycode").val($("#mailingcountrycode").val());
		            		$("#s_option1").val( $("#id").is(':checked') ? '100' : '1500' );
		            		$("#s_option2").val( $("#id").is(':checked') ? '100' : '1500' );
		            		$("#s_option3").val( $("#id").is(':checked') ? '100' : '1500' );
		            		
		            		$("#registerForm").submit();
		            	}
		            }
		            else { return false; }
                });

            }); 
 </script>   
    
 <div class="container-fluid">
  <h1>Preference center</h1>
     <p>Update your preferences</p>           
</div>
    
    
<form id="registerForm" name="preferences" method="post" action="go.aspx">
  <div class="class=form-group">
    <div class="form-group col-md-4">
      <label for="inputEmail4">Email</label>
      <input type="email" class="form-control" id="inputEmail4" placeholder="Email">
    </div>
    <div class="form-group col-md-4" style="left: 0px; top: 0px">
      <label for="inputPassword4">Password</label>
      <input type="password" class="form-control" id="inputPassword4" placeholder="Password">
    </div>
  </div>
  <div class="form-group col-md-4">
    <label for="inputAddress">Address</label>
    <input type="text" class="form-control" id="inputAddress" placeholder="1234 Main St">
  </div>
  <div class="form-group col-md-4">
    <label for="inputAddress2">Address 2</label>
    <input type="text" class="form-control" id="inputAddress2" placeholder="Apartment, studio, or floor">
  </div>
  <div class="form-group col-md-2">
      <label for="inputCity">City</label>
      <input type="text" class="form-control" id="inputCity">
  </div>
    
    <div class="form-group col-md-2">
	<label for="state" class="text-left">State</label>
		<select class="form-control" id="state" name="state">
			<option value="">N/A</option>
			<option value="AK">Alaska</option>
			<option value="AL">Alabama</option>
			<option value="AR">Arkansas</option>
			<option value="AZ">Arizona</option>
			<option value="CA">California</option>
			<option value="CO">Colorado</option>
			<option value="CT">Connecticut</option>
			<option value="DC">District of Columbia</option>
			<option value="DE">Delaware</option>
			<option value="FL">Florida</option>
			<option value="GA">Georgia</option>
			<option value="HI">Hawaii</option>
			<option value="IA">Iowa</option>
			<option value="ID">Idaho</option>
			<option value="IL">Illinois</option>
			<option value="IN">Indiana</option>
			<option value="KS">Kansas</option>
			<option value="KY">Kentucky</option>
			<option value="LA">Louisiana</option>
			<option value="MA">Massachusetts</option>
			<option value="MD">Maryland</option>
			<option value="ME">Maine</option>
			<option value="MI">Michigan</option>
			<option value="MN">Minnesota</option>
			<option value="MO">Missouri</option>
			<option value="MS">Mississippi</option>
			<option value="MT">Montana</option>
			<option value="NC">North Carolina</option>
			<option value="ND">North Dakota</option>
			<option value="NE">Nebraska</option>
			<option value="NH">New Hampshire</option>
			<option value="NJ">New Jersey</option>
			<option value="NM">New Mexico</option>
			<option value="NV">Nevada</option>
			<option value="NY">New York</option>
			<option value="OH">Ohio</option>
			<option value="OK">Oklahoma</option>
			<option value="OR">Oregon</option>
			<option value="PA">Pennsylvania</option>
			<option value="PR">Puerto Rico</option>
			<option value="RI">Rhode Island</option>
			<option value="SC">South Carolina</option>
			<option value="SD">South Dakota</option>
			<option value="TN">Tennessee</option>
			<option value="TX">Texas</option>
			<option value="UT">Utah</option>
			<option value="VA">Virginia</option>
			<option value="VT">Vermont</option>
			<option value="WA">Washington</option>
			<option value="WI">Wisconsin</option>
			<option value="WV">West Virginia</option>
			<option value="WY">Wyoming</option>
		</select>
</div>
    
    <div class="form-group col-md-2">
      <label for="inputZip">Zip</label>
      <input type="text" class="form-control" id="inputZip">
    </div>
     
  
  <div id="option1" class="form-group col-md-4">
    <div class="form-check">
      <input class="form-check-input" type="checkbox" id="gridCheck">
      <label class="form-check-label" for="gridCheck">
        Option 1
      </label>
        </div>
       <div id="option2" class="form-check">
      <input class="form-check-input" type="checkbox" id="gridCheck">
      <label class="form-check-label" for="gridCheck">
        Option 2
      </label>
        </div>
      <div id="option3" class="form-check">
      <input class="form-check-input" type="checkbox" id="gridCheck">
      <label class="form-check-label" for="gridCheck">
        Option 3
      </label>
        </div>
      <div id="option4" class="form-check">
      <input class="form-check-input" type="checkbox" id="gridCheck">
      <label class="form-check-label" for="gridCheck">
        Option 4
      </label>
        </div>
</div>
    
<!---    
    <div class="form-check col-md-4">
  <input class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios1" value="option1" checked>
  <label class="form-check-label" for="exampleRadios1">
    Default radio
  </label>
</div>
<div class="form-check col-md-4">
  <input class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios2" value="option2">
  <label class="form-check-label" for="exampleRadios2">
    Second default radio
  </label>
</div>
<div class="form-check col-md-4">
  <input class="form-check-input" type="radio" name="exampleRadios" id="exampleRadios3" value="option3" disabled>
  <label class="form-check-label" for="exampleRadios3">
    Disabled radio
  </label>
</div> --->

<div class="form-check col-md-2">
  <button id="signin" class="btn btn-primary" type="submit">Sign in</button>
</div>    
  
</form>

</body>
</html>


