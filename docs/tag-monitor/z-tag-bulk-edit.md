# Tag Bulk Edit

## Update all your tags to include the tag name in the meta data


In cases when many GTM tags need to be updated for proper functioning of the Tag Monitor and in order to avoid hours of manual and repetitive work, this guide might be useful. 
Steps to bulk edit your tags:                     

1. Export your GTM containerunder Admin -> Export Container -> YOUR WORKSPACE -> Export.                         

2. Open the downloaded container file in an advanced text editor (like notepad++) and locate the tags block.                      


3. Open a json file named 'tags.json' and paste the tag block into it (wrap the whole tag block in {}) and save it.                          


        
        {
        "tag": []
        }
                         
                                              

4. In VSCode, open an html file and paste the code below into the file.                  
        


        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8">
                <meta http-equiv="X-UA-Compatible" content="IE=edge">
                <title></title>
                <meta name="description" content="">
                <meta name="viewport" content="width=device-width, initial-scale=1">
                <link rel="stylesheet" href="">
            </head>
            <script>
                window.onload = (event) => {
                    function readSingleFile(evt) {
                        var f = evt.target.files[0];
                        if (f) {
                            const r = new FileReader();
                            r.onload = function(e) {
                                const contents = e.target.result;
                                const json = JSON.parse(contents);
                                let beforeCount = 0;

                                json.tag.forEach(el =>
                                    el.monitoringMetadataTagNameKey ? beforeCount++ : undefined);
                                
                                console.log(`We have ${beforeCount} properties in ${json.tag.length} tags`);

                                json.tag.forEach(el =>
                                    el.monitoringMetadataTagNameKey === undefined ? el.monitoringMetadataTagNameKey = "name" : undefined);
                                
                                let afterCount = 0;

                                json.tag.forEach(el =>
                                    el.monitoringMetadataTagNameKey ? afterCount++ : undefined);

                                console.log(`Now we have ${afterCount} properties in ${json.tag.length} tags after the script work done!`);

                                navigator.clipboard.writeText(JSON.stringify(json.tag));

                                alert('Job done! Now you can do Ctrl+V and change the data anywhere you want!')
                            }
                            r.readAsText(f);
                        } else {
                            alert("Failed to load file");
                        }
                    }

                    document.getElementById('fileinput').addEventListener('change', readSingleFile, false);
                }
            </script>
            <body>
                <input id="fileinput" type="file"/>
            </body>
        </html>



5. Run the browser and choose the tags.json file in the input field and, wait until you receive an alert message saying that the job is done. Now the modified tag block is copied into your clipboard. 
6. Format the code block [here](https://jsonformatter.curiousconcept.com) to the standard Json format.
7. Replace the old tag block in the downloaded container file with your updated and formatted block (be mindful of the correct punctuation) and save the file;
8. Import container into your workspace under Admin -> Import Container -> choose container file and workspace -> Overwrite.

You're done. All your tags have been updated!