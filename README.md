#  List proper names of files in a folder 

// set yout folder path

    $BaseDir = "K:/AosService/PackagesLocalDirectory" 

// set your file name
     
    $OutputFile = "table_extensions.csv"  

//Files names extraction 

    "FirstPart" | Set-Content $OutputFile
    Get-ChildItem -Path $BaseDir -Recurse -Directory -Filter "AxTableExtension" | ForEach-Object {
        $axTableExtDir = $_.FullName
        Get-ChildItem -Path $axTableExtDir -File | ForEach-Object {
            $file = $_.FullName
            if (Test-Path $file) {
                $filename = Split-Path $file -Leaf
                $firstPart = $filename.Split('.')[0]
                Add-Content $OutputFile $firstPart
                Write-Host "Exécution du fichier : $file"
            }
      }
    }
   
//Output   
     
     Write-Host "Le nom des Table ont été copiée dans $OutputFile"
