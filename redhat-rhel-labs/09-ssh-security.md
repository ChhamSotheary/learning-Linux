# Lab ៩៖ កំណត់រចនាសម្ព័ន្ធ និងការពារ SSH (Configure and Secure SSH)

## គោលបំណង
យល់ពី SSH client/server, host key, authentication និងការតភ្ជាប់ពី client ទៅ VM។

## ១. ពិនិត្យ SSH tools
```bash
ssh -V
command -v ssh
command -v ssh-keygen
```
SSH ប្រើសម្រាប់ភ្ជាប់ទៅម៉ាស៊ីនពីចម្ងាយដោយការអ៊ិនគ្រីប។

## ២. ពិនិត្យ SSH server
```bash
systemctl status sshd
sudo sshd -t
```
`sshd -t` ពិនិត្យ syntax configuration ប្រសិនបើ server package មានដំឡើង។

## ៣. បង្កើត key pair សម្រាប់ user ផ្ទាល់
```bash
ssh-keygen -t ed25519 -C "rhel-lab-key"
```
ទុកទីតាំង default ប្រសិនបើសមស្រប ហើយកំណត់ passphrase។ Private key មិនត្រូវចែករំលែកឡើយ។ Public key មាន suffix `.pub`។

## ៤. មើល public key
```bash
cat ~/.ssh/id_ed25519.pub
```
ចែករំលែកតែ public key ទៅ server ដែលអ្នកមានសិទ្ធិគ្រប់គ្រង។ កុំបង្ហាញ ឬផ្ញើ `id_ed25519` ដែលគ្មាន `.pub`។

## ៥. ភ្ជាប់ទៅម៉ាស៊ីន
```bash
ssh username@server-address
```
ប្រើ username និង IP/hostname របស់ VM ពិតប្រាកដ។ ពិនិត្យ fingerprint របស់ server តាម channel ដែលទុកចិត្ត មុនទទួលយក host key។

## ៦. លំហាត់
1. ពិនិត្យថា ssh client មានឬអត់។
2. បង្កើត Ed25519 key pair។
3. កំណត់អត្តសញ្ញាណ public key និង private key។
4. ពន្យល់ហេតុអ្វី private key ត្រូវរក្សាសម្ងាត់។

## ពិនិត្យចំណេះដឹង
- [ ] ខ្ញុំយល់ពី SSH client និង server។
- [ ] ខ្ញុំអាចបង្កើត key pair។
- [ ] ខ្ញុំមិនចែករំលែក private key។

**សុវត្ថិភាព:** កុំកែ `/etc/ssh/sshd_config` ឬបិទ password authentication មុនពេលបានសាក key login និងមាន console access ដើម្បីស្ដារវិញ។
