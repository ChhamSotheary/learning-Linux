# Lab ៦៖ គ្រប់គ្រង File Permissions (Control File Permissions)

## គោលបំណង
យល់ពី read (r), write (w), execute (x), owner, group និង permission mode។

## ១. មើល Permission
```bash
ls -l /etc/hosts
```
ឧទាហរណ៍ mode `-rw-r--r--`៖ តួអក្សរដំបូងបង្ហាញប្រភេទ file; បន្ទាប់មកជា permission របស់ owner, group និង others។

## ២. បង្កើត file សាកល្បង
```bash
mkdir -p "$HOME/rhel-labs/lab06"
cd "$HOME/rhel-labs/lab06"
touch example.txt
ls -l example.txt
```

## ៣. ប្រើ chmod ជាទម្រង់និមិត្តសញ្ញា
```bash
chmod u+rw,go-rwx example.txt
ls -l example.txt
chmod u-x example.txt
```
`u` = owner, `g` = group, `o` = others។ សញ្ញា `+`, `-`, `=` បន្ថែម ដក ឬកំណត់ permission។

## ៤. ប្រើ chmod ជាលេខ
```bash
chmod 640 example.txt
ls -l example.txt
```
លេខ 4 = read, 2 = write, 1 = execute។ ដូច្នេះ 640 មានន័យថា owner មាន rw-, group មាន r-- និង others គ្មានសិទ្ធិ។

## ៥. Owner និង Group
```bash
stat example.txt
```
ការប្ដូរ owner/group ដោយ `chown` ជាទូទៅត្រូវការ sudo។ កុំប្ដូរ owner លើ system files សម្រាប់លំហាត់នេះ។

## ៦. លំហាត់
1. បង្កើត file `private.txt` ក្នុង workspace។
2. កំណត់ mode 600។
3. ប្រើ `ls -l` និង `stat` ដើម្បីផ្ទៀងផ្ទាត់។
4. ពន្យល់ថាហេតុអ្វី mode 600 ខុសពី 644។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចអាន rwx។
- [ ] ខ្ញុំអាចកំណត់ mode ជាលេខ និងនិមិត្តសញ្ញា។
- [ ] ខ្ញុំដឹងថា permission មិនដូច ownership ទេ។

**សុវត្ថិភាព:** អនុវត្តតែលើឯកសារដែលអ្នកបង្កើត។ កុំប្រើ `chmod -R` លើ system directories។
