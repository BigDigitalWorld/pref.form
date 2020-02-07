# pref.form
Preference Form - Bootstrap 4

<!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap Form Template</title>
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
    
                                                <input type="hidden" name="cr" value="{(CustomerID)}" />
                                                <input type="hidden" name="fm" value="{(FormID)}" />
                                                <input type="hidden" name="mg" value="{(MessageID)}" />
												<input type="hidden" name="cn" value="{(CampaignID)}" />
												<input type="hidden" id="s_pref01" name="s_pref01" value="{(01pref)}"/>
												<input type="hidden" id="s_pref02" name="s_pref02" value="{(02pref)}"/>
												<input type="hidden" id="s_pref03" name="s_pref03" value="{(03pref)}"/>
												<input type="hidden" id="s_pref04" name="s_pref04" value="{(04pref)}"/>
																															
												<input type="hidden" id="s_dob" name="s_dob" value="{(dob)}"/>
												<input type="hidden" id="s_email" name="s_email" value="{(email)}"/>
												<input type="hidden" id="s_mailingstate" name="s_mailingstate" value="{(mailingstate)}"/>
												<input type="hidden" id="s_mailingcountrycode" name="s_mailingcountrycode" value="{(mailingcountrycode)}"/>

  <div class="class=form-group">
    <div class="form-group col-md-4">
      <label for="inputEmail4" generated="true">Email</label>
      <input type="text" id="s_email_string" name="s_email_string" value="{(email_string)}" class="form-control" placeholder="Email">
    </div>
   
    <div class="form-group col-md-4">
      <label for="inputEmail4" generated="true">First Name</label>
      <input type="text" class="form-control" id="s_firstname" name="s_firstname" value="{(firstname)}" placeholder="s_firstname">
    </div>
 
    <div class="form-group col-md-4">
      <label for="inputEmail4" generated="true">Last Name</label>
      <input type="text" class="form-control" id="s_lastname" value="{(lastname)}" placeholder="Email">
    </div>

  </div>
  <div class="form-group col-md-4">
    <label for="inputAddress" generated="true">Address</label>
    <input type="text" class="form-control" id="s_mailingaddressline1" name="s_mailingaddressline1" value="{(mailingaddressline1)}" placeholder="Address">
  </div>
  <div class="form-group col-md-4">
    <label for="inputAddress2">Address 2</label>
    <input type="text" class="form-control" id="s_mailingaddressline2" name="s_mailingaddressline2" value="{(mailingaddressline2)}" placeholder="Apartment, studio, or floor">
  </div>
  <div class="form-group col-md-2">
      <label for="inputCity" generated="true">City</label>
      <input type="text" class="form-control" id="s_mailingcity" name="s_mailingcity" value="{(mailingcity)}">
  </div>
    
    <div class="form-group col-md-2">
	<label for="state" class="text-left" generated="true">State</label>
		<select class="form-control" id="state" id="mailingstate" value="" name="state">
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
      <label for="inputZip" generated="true">Zip</label>
      <input type="text" class="form-control" id="inputZip">
    </div>
     
    <!--COUNTRY-->

          <div class="form-group col-md-2">
          <label for="Country"  class="text-left" generated="true">Country</label><br>
          <select class="form-control" id="countrycode" name="countrycode" value="">
             <option value="United States">UNITED STATES</option>
             <option value="Afghanistan">AFGHANISTAN</option>
             <option value="Albania">ALBANIA</option>
             <option value="Algeria">ALGERIA</option>
             <option value="American Somoa">AMERICAN SAMOA</option>
             <option value="Andorra">ANDORRA</option>
             <option value="Angola">ANGOLA</option>
             <option value="Anguilla">ANGUILLA</option>
             <option value="Antarctica">ANTARCTICA</option>
             <option value="Antigua and Barbuda">ANTIGUA AND BARBUDA</option>
             <option value="Argentina">ARGENTINA</option>
             <option value="Armenia">ARMENIA</option>
             <option value="Aruba">ARUBA</option>
             <option value="Australia">AUSTRALIA</option>
             <option value="Austria">AUSTRIA</option>
             <option value="Azerbaijan">AZERBAIJAN</option>
             <option value="Bahamas">BAHAMAS</option>
             <option value="Bahrain">BAHRAIN</option>
             <option value="Bangladesh">BANGLADESH</option>
             <option value="Barbados">BARBADOS</option>
             <option value="Belarus">BELARUS</option>
             <option value="Belgium">BELGIUM</option>
             <option value="Belize">BELIZE</option>
             <option value="Benin">BENIN</option>
             <option value="Bermuda">BERMUDA</option>
             <option value="Bhutan">BHUTAN</option>
             <option value="Bolivia">BOLIVIA</option>
             <option value="Bosnia and Herzegovina">BOSNIA AND HERZEGOVINA</option>
             <option value="Botswana">BOTSWANA</option>
             <option value="Bouvet Island">BOUVET ISLAND</option>
             <option value="Brazil">BRAZIL</option>
             <option value="British Indian Ocean Territory">BRITISH INDIAN OCEAN TERRITORY</option>
             <option value="Brunei Darussalam">BRUNEI DARUSSALAM</option>
             <option value="Bulgaria">BULGARIA</option>
             <option value="Burkina Faso">BURKINA FASO</option>
             <option value="Burundi">BURUNDI</option>
             <option value="Cambodia">CAMBODIA</option>
             <option value="Cameroon">CAMEROON</option>
             <option value="Canada">CANADA</option>
             <option value="Cape Verde">CAPE VERDE</option>
             <option value="Cayman Islands">CAYMAN ISLANDS</option>
             <option value="Central African Republic">CENTRAL AFRICAN REPUBLIC</option>
             <option value="Chad">CHAD</option>
             <option value="Chile">CHILE</option>
             <option value="China">CHINA</option>
             <option value="Christmas Island">CHRISTMAS ISLAND</option>
             <option value="Cocos Keeling Islands">COCOS (KEELING) ISLANDS</option>
             <option value="Colombia">COLOMBIA</option>
             <option value="Comoros">COMOROS</option>
             <option value="Congo">CONGO</option>
             <option value="Cook Island">COOK ISLANDS</option>
             <option value="Costa Rica">COSTA RICA</option>
             <option value="Cote D Ivoire">COTE D'IVOIRE</option>
             <option value="Croatia">CROATIA (local name: Hrvatska)</option>
             <option value="Cuba">CUBA</option>
             <option value="Cyprus">CYPRUS</option>
             <option value="Czech Republic">CZECH REPUBLIC</option>
             <option value="Denmark">DENMARK</option>
             <option value="Djibouti">DJIBOUTI</option>
             <option value="Dominica">DOMINICA</option>
             <option value="Dominican Republic">DOMINICAN REPUBLIC</option>
             <option value="East Timor">EAST TIMOR</option>
             <option value="Ecuador">ECUADOR</option>
             <option value="Egypt">EGYPT</option>
             <option value="El Salvador">EL SALVADOR</option>
             <option value="Equatorial Guinea">EQUATORIAL GUINEA</option>
             <option value="Eritrea">ERITREA</option>
             <option value="Estonia">ESTONIA</option>
             <option value="Ethiopia">ETHIOPIA</option>
             <option value="Falkland Islands">FALKLAND ISLANDS (MALVINAS)</option>
             <option value="Faroe Islands">FAROE ISLANDS</option>
             <option value="Fiji">FIJI</option>
             <option value="Finland">FINLAND</option>
             <option value="France">FRANCE</option>
             <option value="France Metropolitan">FRANCE, METROPOLITAN</option>
             <option value="French Guiana">FRENCH GUIANA</option>
             <option value="French Polynesia">FRENCH POLYNESIA</option>
             <option value="French Southern Territories">FRENCH SOUTHERN TERRITORIES</option>
             <option value="Gabon">GABON</option>
             <option value="Gambia">GAMBIA</option>
             <option value="Georgia">GEORGIA</option>
             <option value="Germany">GERMANY</option>
             <option value="Ghana">GHANA</option>
             <option value="Gibraltar">GIBRALTAR</option>
             <option value="Greece">GREECE</option>
             <option value="Greenland">GREENLAND</option>
             <option value="Grenada">GRENADA</option>
             <option value="Guadeloupe">GUADELOUPE</option>
             <option value="Guam">GUAM</option>
             <option value="Guatemala">GUATEMALA</option>
             <option value="Guinea">GUINEA</option>
             <option value="Guinea-Bissau">GUINEA-BISSAU</option>
             <option value="Guyana">GUYANA</option>
             <option value="Haiti">HAITI</option>
             <option value="Heard and Mc Donald Islands">HEARD AND MC DONALD ISLANDS</option>
             <option value="Honduras">HONDURAS</option>
             <option value="Hong Kong">HONG KONG</option>
             <option value="Hungary">HUNGARY</option>
             <option value="Iceland">ICELAND</option>
             <option value="India">INDIA</option>
             <option value="Indonesia">INDONESIA</option>
             <option value="Iran">IRAN (ISLAMIC REPUBLIC OF)</option>
             <option value="Iraq">IRAQ</option>
             <option value="Ireland">IRELAND</option>
             <option value="Israel">ISRAEL</option>
             <option value="Italy">ITALY</option>
             <option value="Jamaica">JAMAICA</option>
             <option value="Japan">JAPAN</option>
             <option value="Jordan">JORDAN</option>
             <option value="Kazakhstan">KAZAKHSTAN</option>
             <option value="Kenya">KENYA</option>
             <option value="Kiribati">KIRIBATI</option>
             <option value="Korea Democratic Peoples Republic Of">KOREA, DEMOCRATIC PEOPLE'S REPUBLIC OF</option>
             <option value="Korea Republic Of">KOREA, REPUBLIC OF</option>
             <option value="Kuwait">KUWAIT</option>
             <option value="Kyrgtyzstan">KYRGYZSTAN</option>
             <option value="Lao Peoples Democratic Republic">LAO PEOPLE'S DEMOCRATIC REPUBLIC</option>
             <option value="Latavia">LATVIA</option>
             <option value="Lebanon">LEBANON</option>
             <option value="Lesotho">LESOTHO</option>
             <option value="Liberia">LIBERIA</option>
             <option value="Libyan Arab Jamahiriya">LIBYAN ARAB JAMAHIRIYA</option>
             <option value="Liechtenstein">LIECHTENSTEIN</option>
             <option value="Lithuania">LITHUANIA</option>
             <option value="Luxembourg">LUXEMBOURG</option>
             <option value="Macau">MACAU</option>
             <option value="Macedonia">MACEDONIA</option>
             <option value="Madagascar">MADAGASCAR</option>
             <option value="Malawi">MALAWI</option>
             <option value="Malaysia">MALAYSIA</option>
             <option value="Maldives">MALDIVES</option>
             <option value="Mali">MALI</option>
             <option value="Malta">MALTA</option>
             <option value="Marshall Islands">MARSHALL ISLANDS</option>
             <option value="Martinique">MARTINIQUE</option>
             <option value="Mauritania">MAURITANIA</option>
             <option value="Mauritius">MAURITIUS</option>
             <option value="Mayotte">MAYOTTE</option>
             <option value="Mexico">MEXICO</option>
             <option value="Micronesia">MICRONESIA, FEDERATED STATES OF</option>
             <option value="Moldova">MOLDOVA, REPUBLIC OF</option>
             <option value="Monaco">MONACO</option>
             <option value="Mongolia">MONGOLIA</option>
             <option value="Montserrat">MONTSERRAT</option>
             <option value="Morocco">MOROCCO</option>
             <option value="Mozambique">MOZAMBIQUE</option>
             <option value="Myanmar">MYANMAR</option>
             <option value="Namibia">NAMIBIA</option>
             <option value="Nauru">NAURU</option>
             <option value="Nepal">NEPAL</option>
             <option value="Netherlands">NETHERLANDS</option>
             <option value="Netherlands Antilles">NETHERLANDS ANTILLES</option>
             <option value="New Caledonia">NEW CALEDONIA</option>
             <option value="New Zealand">NEW ZEALAND</option>
             <option value="Nicaragua">NICARAGUA</option>
             <option value="Niger">NIGER</option>
             <option value="Nigeria">NIGERIA</option>
             <option value="Niue">NIUE</option>
             <option value="Norfolk Island">NORFOLK ISLAND</option>
             <option value="Northern Mariana Islands">NORTHERN MARIANA ISLANDS</option>
             <option value="Norway">NORWAY</option>
             <option value="Oman">OMAN</option>
             <option value="Pakistan">PAKISTAN</option>
             <option value="Palau">PALAU</option>
             <option value="Panama">PANAMA</option>
             <option value="Papua New Guinea">PAPUA NEW GUINEA</option>
             <option value="Paraguay">PARAGUAY</option>
             <option value="Peru">PERU</option>
             <option value="Philippines">PHILIPPINES</option>
             <option value="Pitcairn">PITCAIRN</option>
             <option value="Poland">POLAND</option>
             <option value="Portugal">PORTUGAL</option>
             <option value="Puerto Rico">PUERTO RICO</option>
             <option value="Qatar">QATAR</option>
             <option value="Reunion">REUNION</option>
             <option value="Romania">ROMANIA</option>
             <option value="Russian Federation">RUSSIAN FEDERATION</option>
             <option value="Rwanda">RWANDA</option>
             <option value="Saint Kitts and Nevis">SAINT KITTS AND NEVIS</option>
             <option value="Saint Lucia">SAINT LUCIA</option>
             <option value="Saint Vincent and the Grenadines">SAINT VINCENT AND THE GRENADINES</option>
             <option value="Samoa">SAMOA</option>
             <option value="San Marino">SAN MARINO</option>
             <option value="Sao Tome and Principe">SAO TOME AND PRINCIPE</option>
             <option value="Saudi Arabia">SAUDI ARABIA</option>
             <option value="Senegal">SENEGAL</option>
             <option value="Seychelles">SEYCHELLES</option>
             <option value="Sierra Leone">SIERRA LEONE</option>
             <option value="Singapore">SINGAPORE</option>
             <option value="Slovakia">SLOVAKIA (Slovak Republic)</option>
             <option value="Slovenia">SLOVENIA</option>
             <option value="Solomon Islands">SOLOMON ISLANDS</option>
             <option value="Somalia">SOMALIA</option>
             <option value="South Africa">SOUTH AFRICA</option>
             <option value="South Georgia and the South Sandwich Islands">SOUTH GEORGIA AND THE SOUTH SANDWICH ISLANDS</option>
             <option value="Spain">SPAIN</option>
             <option value="Sri Lanka">SRI LANKA</option>
             <option value="St Helena">ST. HELENA</option>
             <option value="St Pierre And Miquelon">ST. PIERRE AND MIQUELON</option>
             <option value="Sudan">SUDAN</option>
             <option value="Suriname">SURINAME</option>
             <option value="Svalbard and Jan Mayen Islands">SVALBARD AND JAN MAYEN ISLANDS</option>
             <option value="Swaziland">SWAZILAND</option>
             <option value="Sweden">SWEDEN</option>
             <option value="Switzerland">SWITZERLAND</option>
             <option value="Syrian Arab Republic">SYRIAN ARAB REPUBLIC</option>
             <option value="Taiwan">TAIWAN, PROVINCE OF CHINA</option>
             <option value="Tajikistan">TAJIKISTAN</option>
             <option value="Tanzania">TANZANIA, UNITED REPUBLIC OF</option>
             <option value="Thailand">THAILAND</option>
             <option value="Togo">TOGO</option>
             <option value="Tokelau">TOKELAU</option>
             <option value="Tonga">TONGA</option>
             <option value="Trinidad and Tobago">TRINIDAD AND TOBAGO</option>
             <option value="Tunisia">TUNISIA</option>
             <option value="Turkey">TURKEY</option>
             <option value="Turkmenistan">TURKMENISTAN</option>
             <option value="Turks and Caicos Islands">TURKS AND CAICOS ISLANDS</option>
             <option value="Tuvalu">TUVALU</option>
             <option value="Uganda">UGANDA</option>
             <option value="Ukraine">UKRAINE</option>
             <option value="United Arab Emirates">UNITED ARAB EMIRATES</option>
             <option value="United Kingdom">UNITED KINGDOM</option>
             <option value="United Stated Minor Outlying Islands">UNITED STATES MINOR OUTLYING ISLANDS</option>
             <option value="Uruguay">URUGUAY</option>
             <option value="Uzebekistan">UZBEKISTAN</option>
             <option value="Vanuatu">VANUATU</option>
             <option value="Vatican City State">VATICAN CITY STATE (HOLY SEE)</option>
             <option value="Venezuela">VENEZUELA</option>
             <option value="Viet Nam">VIET NAM</option>
             <option value="Virgin Islands British">VIRGIN ISLANDS (BRITISH)</option>
             <option value="Virgin Islands US">VIRGIN ISLANDS (U.S.)</option>
             <option value="Wallis And Futuna Islands">WALLIS AND FUTUNA ISLANDS</option>
             <option value="Western Sahara">WESTERN SAHARA</option>
             <option value="Yemen">YEMEN</option>
             <option value="Yugoslavia">YUGOSLAVIA</option>
             <option value="Zaire">ZAIRE</option>
             <option value="Zambia">ZAMBIA</option>
             <option value="Zimbabwe">ZIMBABWE</option>
             </select>
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
