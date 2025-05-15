## Užduotis 1: Sistemos informacijos gavimas
### Tikslas: Naudotis PowerShell komandomis sistemos informacijos peržiūrai.

### Instrukcija:
- Paleisk PowerShell kaip administratorius.
- Išvesk informaciją apie kompiuterį naudodamas komandą:
    Get-ComputerInfo

- Išvesk tik operacinės sistemos pavadinimą ir versiją:
    Get-ComputerInfo | Select-Object OSName, OSVersion

---
## Užduotis 2: Aplanko sukūrimas ir failo įrašymas
### Tikslas: Mokytis dirbti su failų sistema naudojant PowerShell.

### Instrukcija:
Sukurkite naują aplanką darbalaukyje pavadinimu Testas:
    New-Item -Path "$env:USERPROFILE\Desktop\Testas" -ItemType Directory

Sukurkite teksto failą info.txt šiame aplanke ir įrašykite į jį tekstą „PowerShell veikia!“:
    Set-Content -Path "$env:USERPROFILE\Desktop\Testas\info.txt" -Value "PowerShell veikia!"

## Užduotis 3: Procesų sąrašo peržiūra
### Tikslas: Susipažinti su veikiantys procesais sistemoje.

### Instrukcija:

Peržiūrėkite visus šiuo metu veikiančius procesus:
Get-Process

Raskite ir išveskite tik „notepad“ procesą (jei veikia):
Get-Process -Name notepad

---
## PowerShell skriptas: „Paskutinės valandos klaidų paieška“
### Nustatome laiką – tik paskutinė valanda
$pradziosLaikas = (Get-Date).AddHours(-5)

try {
    # Gauname klaidas (level 2 = Error) iš System log
    $klaidos = Get-WinEvent -FilterHashtable @{
        LogName = 'System'
        Level = 2
        StartTime = $pradziosLaikas
    } | Select-Object TimeCreated, ProviderName, Id, Message

    # Patikriname ar rasta klaidų
    if ($klaidos -and $klaidos.Count -gt 0) {
        Write-Host "`n--- Klaidos per paskutinę valandą ---`n"
        $klaidos | Format-Table -AutoSize
    }
    else {
        Write-Host "Klaidų per paskutinę valandą nerasta."
    }
}
catch {
    Write-Error "Klaida vykdant užklausą: $($_.Exception.Message)"
}
