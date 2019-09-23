## 数据类型错误
* -Integer.MIN_VALUE会重叠，将其转化为long型变量则不会重叠-（long）Integer.MIN_VALUE。
* 字符'1'并不等于整数1，转化方式：'1'-'0'，同理，判断某字符是否为数字时应与'0'和'9'比较，而不是和0和9比较（或者使用Character.isDigit(char a)，a为数字时返回true）。
