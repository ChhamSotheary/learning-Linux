# Lab ១២៖ បង្រួម និងផ្ទេរ Files (Archive and Transfer Files)

## គោលបំណង
បង្កើត archive ដោយ tar, បង្រួមដោយ gzip និងពិនិត្យមាតិកាមុន extract។

## ១. រៀបចំឯកសារសាកល្បង
```bash
mkdir -p "$HOME/rhel-labs/lab12/source"
printf '%s\n' "file one" > "$HOME/rhel-labs/lab12/source/one.txt"
printf '%s\n' "file two" > "$HOME/rhel-labs/lab12/source/two.txt"
```

## ២. បង្កើត tar archive
```bash
cd "$HOME/rhel-labs/lab12"
tar -cvf source.tar source/
tar -tvf source.tar
```
`-c` បង្កើត archive, `-v` បង្ហាញឈ្មោះ, `-f` បញ្ជាក់ archive file។ `-t` រាយមាតិកា។

## ៣. បង្រួមដោយ gzip
```bash
gzip -k source.tar
ls -lh source.tar*
```
`-k` រក្សា file ដើម។ លទ្ធផលជាទូទៅគឺ `source.tar.gz`។

## ៤. Extract ទៅ directory ផ្សេង
```bash
mkdir restore
tar -xzf source.tar.gz -C restore
find restore -type f -print
```
`-x` extract, `-z` gzip, `-f` archive file និង `-C` កំណត់ទីតាំងគោលដៅ។

## ៥. ផ្ទេរឯកសារដោយ scp (ជាជម្រើស)
```bash
scp source.tar.gz username@server-address:/path/to/destination/
```
ប្រើតែ server ដែលអ្នកមានសិទ្ធិចូលប្រើ និងប្ដូរ placeholder ទាំងអស់ទៅតម្លៃពិត។ កុំផ្ញើឯកសារសម្ងាត់ទៅម៉ាស៊ីនមិនទុកចិត្ត។

## លំហាត់
1. បង្កើត archive របស់ source directory។
2. រាយមាតិកា archive ដោយមិន extract។
3. បង្កើត gzip archive។
4. Extract ទៅ directory restore។
5. ផ្ទៀងផ្ទាត់ថាឯកសារដើមទាំងពីរមាននៅក្នុង restore។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំអាចបង្កើត និងមើល tar archive។
- [ ] ខ្ញុំអាចប្រើ gzip។
- [ ] ខ្ញុំអាច extract ទៅទីតាំងជាក់លាក់។
