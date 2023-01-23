#Game of Tones - Markdown

### Getting Started

This is a tutorial document for development of interactive, web-hosted Game of Tones games that explore the basic tonal systems of Oaxacan languages (Santiago Laxopa Zapotec, San Martín Peras Mixtec), as part of the outreach efforts of Nido de Lenguas at UC Santa Cruz.

The TEMPLATE folder contains a number of documents that are ready to use, and require only minimal editing to develop a Game of Tones for the language of interest. The 'img' and 'mp3' folders contain images and audio files (respectively) to use for the playable cards that are dragged and dropped in the game itself. Before getting started, it can be helpful to add your image and audio files to these folders to reference them in the html portions of the game. The 'GoT_Styles.css' document contains all of the styling specifications, which can be freely edited (or replaced entirely) depending on your design preferences.

For the most part, the only files that will require editing are the html files that run each round of the game. These html files reference corresponding JavaScript files, which contain the functions that generate the game cards with appropriate attributes to drag and drop, and three buttons that allow players to restart the game, check their answers, or show the answers and move on to subsequent rounds. These js files allow for the core functions of the current version of the game, and for the most part, should not be edited. That said, more seasoned programmers may feel comfortable editing and developing these files further as they see fit (especially considering that this game was not developed by computer scientists, and can likely be improved upon). This document will briefly cover the functionality of the js component, and highlight portions that can be edited when adding additional tonal patterns in later rounds of the game. 

### JS Files

Lines 1-32 initiate the function which generates the draggable and droppable cards, with positional attributes that track the position of the cards as they are dragged to different playable areas of the game. The documentation for the draggable and droppable interactions from jQuery UI 1.12 can be found [here](https://api.jqueryui.com/1.12/category/interactions/). 

```
			$( init );
			
			//generate draggable and droppable cards with relevant attributes, including their position and current state 
			 
			function init() {
			  	$('.draggable').draggable( {
			  		cursor: 'move',
			  		containment: 'document',
			  		stack: '.draggable',
			  		revert: 'invalid',
			  		snap: '.droppable',
			  		snapMode: 'inner',
			  		snapTolerance: 20
			  	}) .each(function(index){
					//assign position as an attribute
					$(this).attr('data-home-l', $(this).offset().left)
					$(this).attr('data-home-t', $(this).offset().top)
					//initialze the state of the draggable as not in a droppable card
					$(this).attr('boxIn', null)
				});
			  	$('.droppable').droppable( {
			  		accept: '.draggable',
					
    				//call the handleDropEvent function when an item is dropped
					drop: handleDropEvent
    			} ) .each(function(index){
					//initialize the state of the droppable as empty
    				$(this).attr('hasItem', null)
    			});
				
    			$('#cards').droppable( {
			  		accept: '.draggable'
    			} );

```


