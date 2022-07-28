#EasySQL
1.涉及漏洞类型
SQL注入

2.解题思路
题目提示存在SQL注入 => 使用万能密码进行尝试 => 得到flag

3.知识点
SQL注入中的万能密码

原验证登陆语句:

SELECT * FROM admin WHERE Username= '".$username."' AND Password= '".md5($password)."'
输入1' or 1=1 or '1'='1万能密码语句变为:

SELECT * FROM admin WHERE Username='1' OR 1=1 OR '1'='1' AND Password='EDFKGMZDFSDFDSFRRQWERRFGGG'
逻辑运算的优先顺序是NOT>OR>AND

(1.)上面'1'='1' AND Password='EDFKGMZDFSDFDSFRRQWERRFGGG'先计算肯定返回false,因为密码是我们乱输入的。(此处是假)

(2.)Username='1' 返回假,没有用户名是1(此处是假)

(3.)1=1返回真(此处是真)

以上的结果是:   假  or 真 or假  返回真。验证通过。
