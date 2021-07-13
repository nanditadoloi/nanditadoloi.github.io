---
layout: post
title:  "Word Meaning Based Product Search"
---

# Welcome

**Hello world**, this is my first Jekyll blog post.

I hope you like it!

<script src="https://code.jquery.com/jquery-3.5.0.js"></script>
<form action="https://nandita.ddns.net:5000/service" id="searchForm">
  <input type="text" name="s" placeholder="Search...">
  <input type="submit" value="Search">
</form>
<!-- the result of the search will be rendered inside this div -->
<div id="result"></div>
 
<script>
// Attach a submit handler to the form
$( "#searchForm" ).submit(function( event ) {
 
  // Stop form from submitting normally
  event.preventDefault();
  
  var $form = $( this ),
    term = $form.find( "input[name='s']" ).val(),
    url = $form.attr( "action" );
  
  $.ajax({
          type: "POST",
          url: url,
          data: {search:term},
          contentType: "text/json; charset=utf-8",
          dataType: "text",
          success: function (msg) {
          var jsonUpdatedData = msg;}
      });
});
</script>
