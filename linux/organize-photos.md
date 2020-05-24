# Tips for Organization Files in Directories

#### Sort Photos into Directories by Date

```bash
exiftool -r -d %Y/%m "-directory<datetimeoriginal" */*.jpeg
```



#### Find and Remove Empty Directories After Import/Sort

```bash
find . -type d -empty -delete
```



#### Program to Import Photos into Archive Skipping Duplicates

```bash
#! /bin/sh
exiftool -F '-filename<${datetimeoriginal}' -d "%Y/%m/%Y-%m-%d %H.%M.%S.%%e" $1
```



#### Program to Remove Duplicate Images and Rename Photos Based on Date

```bash
#!/bin/sh

printf "|------- Starting Deduplication on %s -----------|\n" $1
if [ -d "$1" ]; then
	cd $1
	
	echo   "|-------- Running Dedup on Uncat Year ---------|"
	exiftool -F -directory=output/ '-filename<${datetimeoriginal}' -d "%Y-%m-%d %H.%M.%S.%%e" .
	echo   "|------- Removing Duplicated Files -------|"
	rm *
	echo   "|------- Copying Original Files ----------|"
	cp output/* .
	echo   "|------ Removing Output Directory --------|"
	rm -r output/
	
	echo   "|-------- Finished Dedup on Uncat Year ---------|"
	
	for MONTH in {01..12}
	do
	  if [ -d "$MONTH" ]; then
	    cd $MONTH	
	    
	    printf "|---------- Starting Month [%s] ----------|\n" $MONTH
	    echo   "|-------- Starting Deduplication ---------|"
	    exiftool -F -directory=output/ '-filename<${datetimeoriginal}' -d "%Y-%m-%d %H.%M.%S.%%e" .
	    
	    echo   "|------- Removing Duplicated Files -------|"
	    rm *
	    
	    echo   "|------- Copying Original Files ----------|"
	    cp output/* .
	    
	    echo   "|------ Removing Output Directory --------|"
	    rm -r output/
	    
	    cd ..
	    printf "|-------- Completed Month [%s] -----------|\n" $MONTH
	    
	    fi
	done
			
fi

printf "|------- Finished Deduplication on %s -----------|\n" $1
```


