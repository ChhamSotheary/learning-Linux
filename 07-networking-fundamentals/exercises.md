# លំហាត់មេរៀនទី ៧៖ Networking Fundamentals

## ផ្នែក A៖ សំណួរ

1. IP address, gateway និង DNS មានតួនាទីអ្វី?
2. TCP និង UDP ខុសគ្នាជាគោលការណ៍ដូចម្តេច?
3. តើ ss -tuln បង្ហាញអ្វី?
4. ហេតុអ្វី ping មិនឆ្លើយតប មិនបញ្ជាក់ថា host down?
5. តើការមើល listening port អាចបញ្ជាក់ថាវាបើកចូលពី Internet បានទេ?

## ផ្នែក B៖ អនុវត្តលើម៉ាស៊ីនរបស់អ្នក

~~~bash
ip link
ip addr
ip route
getent hosts example.com
ss -tuln
~~~

សរសេរ៖
- Interface ដែល active។
- IP address/prefix របស់វា។
- តើមាន default route ឬអត់។
- DNS address ដែល example.com បកប្រែទៅ (វាអាចប្រែប្រួល)។
- ចំនួន listening sockets ដែលបង្ហាញ។

Optional: ប្រសិនបើគោលការណ៍ network អនុញ្ញាត សាក ping ទៅ host ដែលអ្នកគ្រប់គ្រង។ កុំ scan network ឬបញ្ជូន traffic ទៅប្រព័ន្ធដែលគ្មានការអនុញ្ញាត។

## លក្ខខណ្ឌបញ្ចប់

- អាចមើល interface, addresses និង routes។
- អាចពន្យល់ DNS, gateway និង ports។
- អាចបកស្រាយថា firewall/network policy អាចប៉ះពាល់លទ្ធផល។
- អនុវត្តតែក្នុង network ដែលអ្នកមានសិទ្ធិ។
