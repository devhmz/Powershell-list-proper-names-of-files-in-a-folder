$BaseDir = "K:/AosService/PackagesLocalDirectory"
$OutputFile = "table_extensions.csv"
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
Write-Host "Le nom des Table ont été copiée dans $OutputFile"