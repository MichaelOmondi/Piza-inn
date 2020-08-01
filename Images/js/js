 window.onscroll = function() {scrollFunction()};

 function scrollFunction() {
   if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
     document.getElementById("navbar").style.top = "0";
   } else {
     document.getElementById("navbar").style.top = "20px";
   }
 }

// constructor for the order
function Order(name,email,size,crust,toppings){
  this.Name = name;
  this.Email = email;
  this.Size = size;
  this.Crust = crust;
  this.Toppings = toppings;
  this.Addresses = [];

};

// constructor for the address
function Address(area,estate,apartment,door){
  this.Area = area;
  this.Estate = estate;
  this.Apartment = apartment;
  this.Door = door;
};

$("#delivery").click(function(){
  alert("Our Delivery fee is KSh.150");
  $(".addr").show();
  $(".addrss").show();
});

//this is the form submission event
$("form#new-order").submit(function(event) {
  event.preventDefault();

  //this is the data from the form
  var name = $("input#name").val();
  var email = $("input#email").val();

  var crust = $("select#IG2").val();
  var size = $("select#IG1").val();
  var top = [];
  $.each($("input[name='topping']:checked"), function(){
      top.push($(this).val());
  });

  var area = $("input#area").val();
  var estate = $("input#estate").val();
  var apartment = $("input#apartment").val();
  var door = $("input#door").val();


  // this is the constructor for Order(name,phone,size,crust,toppings)

  var newOrder = new Order(name,email,size,crust,top);
  console.log(newOrder);


  // this is the constructor for Address(street,estate,apartment,floor)

  var newAddress = new Address(area,estate,apartment,door);
  console.log(newAddress);
  newOrder.Addresses.push(newAddress);


  billCalculation(newOrder);

  displayData(newOrder);

  // this is the array for the orders

  var totalOrders = [];
  totalOrders.push(newOrder);
  console.log(totalOrders);


  //  clicking submit will empty the fields

  resetFields();

});


// CALC function

function billCalculation(newOrder){
  var sizePrice = parseInt(newOrder.Size.split(", ")[1]);
  console.log(sizePrice);

  var crustPrice = parseInt(newOrder.Crust.split(", ")[1]);
  console.log(crustPrice);

  
  var topp = newOrder.Toppings;
  console.log(topp);

  var toppingPrice = 0;

  // for getting toppings
  for(var i = 0; i < topp.length; i++ ){
      var unitPrice = parseInt(topp[i].split(", ")[1]);

      toppingPrice += unitPrice;
  }
  
  function deliveryFee(){
      var delivery = newOrder.Addresses;
      console.log(delivery);
      var deliveryPrice;

      if(delivery[0].Estate==null || delivery[0].Estate=="" && delivery[0].Street==null || delivery[0].Street=="" && delivery[0].Apartmant==null || delivery[0].Apartmant=="" && delivery[0].Floor==null || delivery[0].Floor==""){
          deliveryPrice = 0;
          return deliveryPrice;
      }else{
          deliveryPrice = 150;
          return deliveryPrice;
      };
  }

  var deliveryTag = deliveryFee();
  console.log(deliveryTag);

  var price = sizePrice + crustPrice + toppingPrice + deliveryTag;
  console.log(price);

  // this is the total after the CALC function

  $("#total").text(price);

}



//this is the function for displaying  data

function displayData(newOrder){
  var name = newOrder.Name;
  var email = newOrder.Email;

  var sze = newOrder.Size.split(", ")[0];
  var szePrc = newOrder.Size.split(", ")[1];

  var crst = newOrder.Crust.split(", ")[0];
  var crstPrc = newOrder.Crust.split(", ")[1];

  var toppngs;
  var toppngsPrc;

  var tops = newOrder.Toppings;
  tops.forEach(function(topps) {
     
      toppngs = topps.split(", ")[0];
      toppngsPrc = topps.split(", ")[1]; 

      // this is the list of arrays

      $("ul#new-topping").append("<li><span class=''>" + toppngs + " " + " @KSh." + toppngsPrc + "</span></li>");
  });

  // a display for the (name,email,size,crust)

  $("#new-name").text(name);
  $("#new-email").text(email);
  $("#new-size").text(sze + " @KSh." + szePrc);
  $("#new-crust").text(crst + " @KSh." + crstPrc);

  //ths is for printing the address


  var ad = newOrder.Addresses;
  $("#new-estate").text(ad[0].Estate);
  $("#new-area").text(ad[0].Area);
  $("#new-apartment").text(ad[0].Apartment);
  $("#new-door").text(ad[0].Door);

}

// for emptying the fields
function resetFields(){
  $("input#name").val("");
  $("input#email").val("");
  $("input[name='topping']").prop('checked',false);
  $("select#IG2").val("");
  $("select#IG1").val("");
  $("input#area").val("");
  $("input#estate").val("");
  $("input#apartment").val("");
  $("input#door").val("");
};