# To show an alert message in a Modal Dialog Box in SharePoint
```
<html>
<head>
<script type="text/javascript" src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
<style>
.hidden {
	display: none;
}
</style>
</head>
<body>
<div id="CustomMessage" class="hidden">
   <h1>
      This site has been moved to a new SharePoint site. You will be redirected to new site shortly. If not redirected, please click <a href="https://www.google.com/" target="_blank">here</a> to go to new site.
   </h1>
</div>
</body>
</html>
<script>
/* function to check if page is in edit mode in SharePoint */
function checkIfPageInEditMode() {
var isPageInEditMode = SP.Ribbon.PageState.Handlers.isInEditMode();
if(!isPageInEditMode) {
SP.SOD.executeFunc('sp.js', 'SP.ClientContext',displaySiteMigratedAlert); 
}
setTimeout(function(){ window.location.href = "https://www.google.com/"; }, 3000); 
}
/* function to display alert message in SharePoint Dialogbox */
function displaySiteMigratedAlert() {
	SP.UI.ModalDialog.showModalDialog({
		title: "Alert!!!",
		width: 900,
		height: 200,
		html: document.getElementById("CustomMessage")
	});
	$("#CustomMessage").removeClass("hidden");
}
			
$(document).ready(function() {
/* wait until page is loaded fully */
ExecuteOrDelayUntilScriptLoaded(checkIfPageInEditMode, "sp.ribbon.js");
});
</script>
```
