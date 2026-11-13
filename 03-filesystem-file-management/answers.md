# ចម្លើយណែនាំ៖ មេរៀនទី ៣

## ផ្នែក A

1. Root directory គឺ /។
2. Absolute path ចាប់ផ្ដើមពី / និងមិនពឹងទីតាំងបច្ចុប្បន្ន។ Relative path បកស្រាយពី working directory បច្ចុប្បន្ន។
3. ls -a រួមបញ្ចូល hidden names ដែលចាប់ផ្ដើមដោយ dot។
4. cp ចម្លង file/directory (តាម options ដែលប្រើ)។ mv ផ្លាស់ទី ឬប្ដូរឈ្មោះ។ វាអាចមានផលប៉ះពាល់លើ destination ដែលមានស្រាប់ ដូច្នេះត្រូវពិនិត្យជាមុន។
5. * ជាទូទៅ match អក្សរច្រើនតួក្នុង filename។ Shell ពង្រីក pattern មុន command ទទួល arguments។

## ផ្នែក B

លទ្ធផលជាក់លាក់អាស្រ័យលើ username និងប្រព័ន្ធ៖

- pwd នឹងបង្ហាញ path របស់ exercise-03។
- Absolute path ទៅ reports គឺ $HOME/linux-practice/exercise-03/reports បន្ទាប់ពី shell ពង្រីក $HOME។
- Relative path ពី exercise-03 ទៅ reports គឺ reports។
- Filename ដែលមាន space ត្រូវ quotes ដើម្បីឱ្យ shell បញ្ជូនវាជា argument តែមួយ មិនបំបែកជាច្រើនពាក្យ។

ពិនិត្យលទ្ធផលក្នុងម៉ាស៊ីនរបស់អ្នកដោយ ls -la និង find។ កុំយក path គំរូដែលមាន username ផ្សេងមកចាត់ទុកជាលទ្ធផលពិតរបស់អ្នក។
