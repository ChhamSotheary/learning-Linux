# ចម្លើយណែនាំ៖ មេរៀនទី ២

ចម្លើយនេះជាគំរូ។ លទ្ធផល command អាចខុសគ្នាតាមប្រព័ន្ធរបស់អ្នក។

## ផ្នែក A

1. Terminal ជាកម្មវិធីបង្ហាញ prompt និងទទួលអត្ថបទ។ Shell ជាកម្មវិធីបកស្រាយ command និងបញ្ជូនការងារទៅប្រព័ន្ធ។
2. ls ជា command, -l ជា option និង /etc ជា argument/path។
3. Exit status 0 ជាទូទៅមានន័យថា command បានបញ្ចប់ដោយជោគជ័យ។
4. Single quotes បង្ហាញអក្សរ $HOME តាមតួអក្សរ។ Double quotes អនុញ្ញាតឱ្យ Bash ពង្រីក variable ទៅតម្លៃ home directory។
5. Tab completion ជួយបំពេញឈ្មោះ command/path។ History ជួយរកមើល និងប្រើ command ដែលបានរត់មុន។

## ផ្នែក B

- echo "$SHELL" បង្ហាញ shell ដែលបានកំណត់ក្នុង environment។
- ps -p "$$" -o comm= បង្ហាញឈ្មោះ process របស់ shell ដែលកំពុងរត់។
- type cd បង្ហាញថា cd ជា shell built-in ក្នុង Bash ជាទូទៅ។
- command -v ls បង្ហាញទីតាំង ឬប្រភេទ command ដែលនឹងត្រូវហៅ។
- printf '%s
' '$HOME' បង្ហាញអក្សរ $HOME។
- printf '%s
' "$HOME" បង្ហាញតម្លៃ home directory។
- true ជាទូទៅមាន exit status 0។
- false ជាទូទៅមាន exit status មិនសូន្យ។
- man ls បើក manual ហើយ q ចេញពីវា។

## ផ្នែក C

1. Command អាចកែ ឬលុបឯកសារ ហើយ arguments អាចប្ដូរផលប៉ះពាល់។
2. sudo ដំណើរការជាមួយសិទ្ធិខ្ពស់។ Command លុប/recursive អាចប៉ះទិន្នន័យច្រើន។ ត្រូវយល់ច្បាស់អំពី target និងផលប៉ះពាល់។
3. ប្រើ VM, container ឬ test directory ដែលគ្មានទិន្នន័យសំខាន់។ កុំសាកល្បងលើប្រព័ន្ធដែលអ្នកមិនមានសិទ្ធិ។

**ចំណាំ៖** ពិនិត្យ manual និង environment ព្រោះ shell និង options អាចខុសគ្នារវាង distributions។
