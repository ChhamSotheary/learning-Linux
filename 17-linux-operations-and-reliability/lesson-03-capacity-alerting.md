# មេរៀនទី ៣៖ Capacity, Alert និង SLO

Capacity planning ពិនិត្យ trend របស់ CPU, memory, storage, I/O និង network ជាមួយ growth និង peak workload។ Alert គួរត្រូវបានភ្ជាប់នឹងផលប៉ះពាល់អ្នកប្រើ ឬ saturation ដែលមានន័យ មិនមែនរាល់ metric ខ្ពស់មួយភ្លែត។

SLO ជាគោលដៅភាពអាចទុកចិត្តបានសម្រាប់សេវា (ឧទាហរណ៍ availability/latency); error budget ជួយសម្រេចថាតើគួរផ្តោត reliability ឬ feature។ ការកំណត់ SLO ត្រូវផ្អែកលើ requirement របស់អ្នកប្រើ មិនមែនចម្លងតម្លៃទូទៅ។

## លំហាត់

1. ជ្រើស metric មួយ និងកំណត់ baseline/seasonality។
2. សរសេរ alert ដែលបញ្ជាក់ scope, threshold, duration, impact និង runbook។
3. បញ្ជាក់ហានិភ័យ false positive និង alert fatigue។
