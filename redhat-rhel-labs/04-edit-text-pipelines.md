# Lab ៤៖ កែសម្រួលអត្ថបទ និងប្រើ Pipelines (Edit Text and Use Pipelines)

## គោលបំណង
- បង្កើត និងកែសម្រួល text file។
- ប្រើ `cat`, `less`, `head`, `tail`។
- ភ្ជាប់ commands ដោយ pipe `|`។
- ត្រង និងតម្រៀបអត្ថបទដោយ `grep`, `sort`, `uniq`, `wc`។

## ១. រៀបចំឯកសារសាកល្បង
```bash
mkdir -p "$HOME/rhel-labs/lab04"
cd "$HOME/rhel-labs/lab04"
cat > servers.txt <<'EOF'
web01 running
db01 stopped
web02 running
cache01 running
db02 stopped
EOF
```
Here-document បញ្ចូលអត្ថបទច្រើនបន្ទាត់ទៅក្នុង file។ ឈ្មោះ `EOF` អាចជាអត្ថបទបិទបញ្ចប់ដែលជ្រើសរើសបាន។

## ២. មើល និងកែសម្រួល
```bash
cat servers.txt
less servers.txt
head -n 2 servers.txt
tail -n 2 servers.txt
```
សាកបើក `nano servers.txt` ប្រសិនបើ nano បានដំឡើង។ រក្សាទុក និងចេញតាមសេចក្ដីណែនាំនៅខាងក្រោម editor។

## ៣. ត្រង និងរាប់
```bash
grep running servers.txt
grep -i stopped servers.txt
wc -l servers.txt
sort servers.txt
```
`grep` ស្វែងរកបន្ទាត់ដែលត្រូវនឹង pattern។ `wc -l` រាប់បន្ទាត់។ `sort` តម្រៀបបន្ទាត់តាមលំដាប់អក្សរ។

## ៤. Pipeline
```bash
grep running servers.txt | sort
grep stopped servers.txt | wc -l
```
Pipe `|` បញ្ជូន output របស់ command ខាងឆ្វេងទៅជា input របស់ command ខាងស្ដាំ។ លទ្ធផល command ទីពីរនៅទីនេះរាប់ចំនួនបន្ទាត់ដែលមាន stopped។

## លំហាត់
1. បន្ថែម server មួយទៅ `servers.txt` ដោយប្រើ editor។
2. បង្ហាញតែ server ដែល running។
3. រាប់ server ដែល stopped។
4. តម្រៀបបញ្ជីទាំងមូល។
5. ពន្យល់ពីលំហូរទិន្នន័យក្នុង `grep running servers.txt | sort`។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចមើល file ដោយ `less`។
- [ ] ខ្ញុំអាចស្វែងរកបន្ទាត់ដោយ `grep`។
- [ ] ខ្ញុំអាចភ្ជាប់ commands ដោយ pipe។

**សុវត្ថិភាព៖** ប្រើតែ file សាកល្បងនេះ។ `>` អាចសរសេរជំនួស file ចាស់។
