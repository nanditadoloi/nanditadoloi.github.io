---
layout: post
title:  "(Demo) Word Meaning Based Product Search"
---
<script src="https://code.jquery.com/jquery-3.5.0.js"></script>
<p>When potential customers search for items on an e-commerce website, they search words they use might not exactly match with the key-words or item-names in the database of the website. So, if the search method only matches the text strings, most likely, the search results mights not be correct. For example if the user is looking for "checkered" shirts, but if search for the word "boxed" instead, they will not get checkered shirts, even if they tried to mean the same thing.</p>

<p>Therefore, in this demo I use Natural Language Processing in an attempt to provide better search results. The backend developed in AWS Lambda searches for meaning insted of simply matching the text. Saw that we are an e-commerce website selling clothes, and the items that we have have these keywords associated with them: "checkered", "plain", "modern", "vintage", "ethnic", "casual", "formal". In this demo, we will pick two of these keywords which mean the most similar to the searched keyword. Once we know these two keywords, we can show the user the products which belong to these keywords.</p>


<p>I use 'text8' model to find similar meaning. This model was not used for this task but was developed to understand the meanings in English words. Therefore the meanings might not be accurate in this context. With custom e-commerce dataset, we can train a more accurate model based on the context which would work far better.</p>

# Demo
Enter a one-word search term into the search box and submit "Search". The most similar keywords would be displayed over the blanks below. Suggestion: Try the search term: "boxed"

<form action="https://nandita.ddns.net:5000/service" id="searchForm">
  <input type="text" name="s" placeholder="Search...">
  <input type="submit" value="Search">
</form>
<!-- the result of the search will be rendered inside this div -->

<hr><br><br>
<h4>The two closest keywords are:</h4>
<strong><span id="result1">____________</span></strong>, and <strong><span id="result2">____________</span></strong>
 
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
          data: JSON.stringify({search:term}),
          contentType: "text/json; charset=utf-8",
          dataType: "text",
          success: function (msg) {
          var jsonUpdatedData = JSON.parse(msg);
          if(jsonUpdatedData.done=="True"){
              $("#result1").text(jsonUpdatedData.data[0]);
              $("#result2").text(jsonUpdatedData.data[1]);
          }
          else{alert("The input data format is incorrect.");}
          }
      });
});
</script>
