# លំហាត់មេរៀនទី ៣៖ Filesystem និងការគ្រប់គ្រងឯកសារ

សូមអនុវត្តតែក្នុង workspace សាកល្បងនៅក្នុង home directory។

## ផ្នែក A៖ សំណួរ

1. តើ root directory របស់ Linux មានឈ្មោះអ្វី?
2. Absolute path ខុសពី relative path ដូចម្តេច?
3. តើ ls -a បង្ហាញអ្វីបន្ថែម?
4. តើ cp និង mv ខុសគ្នាដូចម្តេច?
5. តើ wildcard * អាចពង្រីកទៅជាអ្វី?

## ផ្នែក B៖ អនុវត្ត

រត់ជំហានខាងក្រោម៖

~~~bash
mkdir -p "$HOME/linux-practice/exercise-03"
cd "$HOME/linux-practice/exercise-03"
mkdir reports
touch "weekly notes.txt"
printf '%s
' "Practice file" > "weekly notes.txt"
cp "weekly notes.txt" reports/weekly-copy.txt
find "$HOME/linux-practice/exercise-03" -maxdepth 2 -type f -print
ls -la
~~~

បន្ទាប់មកសរសេរ៖
- លទ្ធផល pwd។
- Absolute path ទៅ reports directory។
- Relative path ពី exercise-03 ទៅ reports។
- តើហេតុអ្វី filename ដែលមាន space ត្រូវបានដាក់ក្នុង quotes?

កុំប្រើ rm ឬ sudo ក្នុងលំហាត់នេះ។

## លក្ខខណ្ឌបញ្ចប់

- អាចបង្កើត directory និង files ក្នុង workspace។
- អាចប្រើ cp, mv, ls និង find លើទិន្នន័យសាកល្បង។
- អាចពន្យល់ absolute/relative path និង wildcard។
- អាចបញ្ជាក់មូលហេតុដែលត្រូវប្រយ័ត្នមុនលុបឯកសារ។
