# លំហាត់មេរៀនទី ២៖ Terminal និង Command Line

សាកល្បងដោយខ្លួនឯង មុនពិនិត្យចម្លើយណែនាំ។

## ផ្នែក A៖ យល់ពាក្យ

1. Terminal និង Shell ខុសគ្នាដូចម្តេច?
2. ក្នុង command ls -l /etc តើមួយណាជា command, option និង argument?
3. តើ exit status 0 ជាទូទៅមានន័យដូចម្តេច?
4. តើភាពខុសគ្នារវាង '$HOME' និង "$HOME" ក្នុង Bash គឺអ្វី?
5. តើ Tab completion និង history ជួយការងារយ៉ាងដូចម្តេច?

## ផ្នែក B៖ អនុវត្ត

រត់ និងកត់ត្រាលទ្ធផល៖

~~~bash
echo "$SHELL"
ps -p "$$" -o comm=
type cd
command -v ls
printf '%s
' '$HOME'
printf '%s
' "$HOME"
true
echo "$?"
false
echo "$?"
~~~

បន្ទាប់មកបើក manual ដោយ man ls ហើយចេញដោយ q។

## ផ្នែក C៖ គិតអំពីសុវត្ថិភាព

1. តើហេតុអ្វីត្រូវអាន command មុន copy/paste?
2. តើ command ដែលមាន sudo ឬលុបទិន្នន័យត្រូវប្រយ័ត្នអ្វីខ្លះ?
3. តើអ្នកអាចសាកល្បង command ដែលមិនស្គាល់ក្នុងបរិស្ថានណាដែលមានហានិភ័យទាប?

## លក្ខខណ្ឌបញ្ចប់

- អាចបំបែក command, options និង arguments។
- អាចប្រើ quotes និងពន្យល់ shell expansion មូលដ្ឋាន។
- អាចពិនិត្យ exit status ភ្លាមៗក្រោយ command។
- អាចបើក/ចេញពី manual និងប្រើ Tab completion។
