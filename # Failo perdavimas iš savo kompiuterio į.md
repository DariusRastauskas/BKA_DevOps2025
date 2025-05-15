# Failo perdavimas iš savo kompiuterio į nuotolinį serverį:
scp dokumentas.pdf vartotojas@serverio_adresas:/namu/katalogas/

# Failo parsisiuntimas iš serverio į savo kompiuterį:
scp vartotojas@serverio_adresas:/namu/katalogas/dokumentas.pdf 

# Viso katalogo kopijavimas (rekursyviai):
scp -r projektas/ vartotojas@serverio_adresas:/home/vartotojas/

