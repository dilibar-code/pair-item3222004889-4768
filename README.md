# pair-item3222004889-4768
this is pair item
package fourcalculations;

import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
        while(true) {
       
            int n = 10;
            int r = 10;
            String submitPath = null;
            String answersPath = null;

            try {
                // 输入题目个数、数字范围
                System.out.println("生成题目请输入 -n 题目数 -r 数字范围"
                		+ "   校验答案请输入 -e 答题文件路径 -a 正确答案文件路径");
                Scanner command = new Scanner(System.in);
                String arr[] = command.nextLine().split("\\s");

                //获取指令相应参数
                if (arr.length > 1) {
                    for (int i = 0; i < arr.length; i = i + 2) {
                        switch (arr[i]) {
                            case "-n":
                                n = Integer.parseInt(arr[i + 1]);
                                if (n > 10000 || n < 1) {
                                    System.out.println("对不起，只允许输入1-10000的数字！");
                                    return; 
                                }
                                break;
                            case "-r":
                                r = Integer.parseInt(arr[i + 1]);
                                if (r < 1) {
                                    System.out.println("对不起，只允许大于等于1的自然数！");
                                    return;
                                }
                                break;
                            case "-e":
                                submitPath = arr[i + 1];
                                if (submitPath == null) {
                                    System.out.println("对不起，没有输入相应文件路径，请重新输入");
                                    return; 
                                }
                                break;
                            case "-a":
                                answersPath = arr[i + 1];
                                if (answersPath == null) {
                                    System.out.println("对不起，没有输入相应文件路径，请重新输入");
                                    return; 
                                }
                                break;
                            default:
                                System.out.println("指令输入错误!");
                                break;
                        }
                    }
                }
            } catch (NumberFormatException e) {
                System.out.println("您输入的指令有误，请重新输入");
            }

            /* ****执行函数 **** */
            System.out.println("n: " + n + ", r: " + r);
            problemSet makefile = new problemSet();
            if (submitPath != null && answersPath != null)
                makefile.createGradeFile(submitPath,answersPath);
            else
                makefile.createProblemSet(n,r);
        }
    }
}

main类
package fourcalculations;

import java.util.Scanner;

public class Main {
	public static void main(String[] args) {
        while(true) {
       
            int n = 10;
            int r = 10;
            String submitPath = null;
            String answersPath = null;

            try {
                // 输入题目个数、数字范围
                System.out.println("生成题目请输入 -n 题目数 -r 数字范围"
                		+ "   校验答案请输入 -e 答题文件路径 -a 正确答案文件路径");
                Scanner command = new Scanner(System.in);
                String arr[] = command.nextLine().split("\\s");

                //获取指令相应参数
                if (arr.length > 1) {
                    for (int i = 0; i < arr.length; i = i + 2) {
                        switch (arr[i]) {
                            case "-n":
                                n = Integer.parseInt(arr[i + 1]);
                                if (n > 10000 || n < 1) {
                                    System.out.println("对不起，只允许输入1-10000的数字！");
                                    return; 
                                }
                                break;
                            case "-r":
                                r = Integer.parseInt(arr[i + 1]);
                                if (r < 1) {
                                    System.out.println("对不起，只允许大于等于1的自然数！");
                                    return;
                                }
                                break;
                            case "-e":
                                submitPath = arr[i + 1];
                                if (submitPath == null) {
                                    System.out.println("对不起，没有输入相应文件路径，请重新输入");
                                    return; 
                                }
                                break;
                            case "-a":
                                answersPath = arr[i + 1];
                                if (answersPath == null) {
                                    System.out.println("对不起，没有输入相应文件路径，请重新输入");
                                    return; 
                                }
                                break;
                            default:
                                System.out.println("指令输入错误!");
                                break;
                        }
                    }
                }
            } catch (NumberFormatException e) {
                System.out.println("您输入的指令有误，请重新输入");
            }

            /* ****执行函数 **** */
            System.out.println("n: " + n + ", r: " + r);
            problemSet makefile = new problemSet();
            if (submitPath != null && answersPath != null)
                makefile.createGradeFile(submitPath,answersPath);
            else
                makefile.createProblemSet(n,r);
        }
    }
}

 CheckRepeat
package fourcalculations;

import java.util.ArrayList;
import java.util.Arrays;

public class CheckRepeat {
	private ArrayList<String> returnList = new ArrayList<>();
    private ArrayList<String> txtList = new ArrayList<>();
    private ArrayList<String> ansList = new ArrayList<>();
    private ArrayList<String[]> ansFoList = new ArrayList<>();

    /**
     * 生成暂存题集、答案集
     * @param n 为 需要的式子总数
     * @param r 为 式子中操作数的范围
     * @return returnList 为 题集&答案集
     */
    public ArrayList generate(int n,int r) {
        Create create = new Create();
        //生成n条不重复的式子
        for(int i=0;i<n;){
            //随机生成式子
            String[] ansFormula = create.createFormula(r);
            //判断生成的式子是否重复-n 10000 -r 1
            if (ansFormula!=null) {
                //System.out.println("generFormula:"+ansFormula[ansFormula.length-1]);
                if (!ifRepeat(ansFormula)) {
                    System.out.println((i+1)+":"+ansFormula[ansFormula.length-1]);
                    i++;
                }
            }
        }

        //把式子及运算结果添加到returnList
        for (int i =0; i<2*n;i++) {
            if(i<n) {
                returnList.add(txtList.get(i));
            } else {
                returnList.add(ansList.get(i - n));
            }
        }
        return returnList;
    }

    /**
     * 判断式子是否重复
     * @param ansFormula 为 后缀表达式、运算结果、式子 的 数组
     * @return ifRepeat 表示当前式子是否重复
     */
    private boolean ifRepeat(String[] ansFormula) {
        String formula = ansFormula[ansFormula.length-1];
        String[] rPNotation = new String[ansFormula.length-1];
        System.arraycopy(ansFormula, 0, rPNotation, 0, ansFormula.length-1);
        boolean ifRepeat = false;

        for (String[] ansFo: ansFoList) {
            if (Arrays.equals(ansFo,rPNotation)) { //直接一一对应比较
                ifRepeat = true;
                //System.out.println("ansFo==rPNotation:"+Arrays.toString(ansFo)+"=="+Arrays.toString(rPNotation));
            } else if (ansFo.length == rPNotation.length && ansFo[ansFo.length-1].equals(rPNotation[rPNotation.length-1])){//若运算结果及长度一致，则式子可能重复，进一步比较
                int j=0;
                for (j=0;j<rPNotation.length-2;) {
                    //System.out.println(Arrays.toString(ansFo)+":"+Arrays.toString(rPNotation));
                    boolean opRight = ansFo[j+2].equals("＋")||ansFo[j+2].equals("×");
                    boolean exRight = ansFo[j].equals(rPNotation[j + 1]) && ansFo[j + 1].equals(rPNotation[j]) && ansFo[j + 2].equals(rPNotation[j + 2]);
                    boolean copRight = ansFo[j].equals(rPNotation[j]) && ansFo[j + 1].equals(rPNotation[j + 1]) && ansFo[j + 2].equals(rPNotation[j + 2]);
                    //运算符前后两个操作数交换比较
                    if (exRight&&opRight) {
                        j = j + 3;
                    } else if (copRight) {
                        j = j + 3;
                    } else {
                        //System.out.println(formula+":"+opRight+","+exRight+","+"false ;j:"+j+"<---->ifRepeat:false");
                        break;
                    }
                    //System.out.print(formula+":"+opRight+","+exRight+","+copRight+"  ;");
                }
                if (j == rPNotation.length-2) {
                    ifRepeat = true;
                    break;
                }
                //System.out.println("j:"+j+",rPNotation.length-5:"+(rPNotation.length-5)+"<---->ifRepeat:" + ifRepeat);
            }
        }

        if (!ifRepeat) {
            this.txtList.add(formula);
            this.ansList.add(rPNotation[rPNotation.length-1]);
            this.ansFoList.add(rPNotation);
        }
        return ifRepeat;
    }

}

package fourcalculations;

import java.util.HashMap;
import java.util.Stack;

public class CheckAnswer {
	  /**
     * 检查式子结果、生成逆波兰表达式
     * @param formula 为 式子
     * @return reversePolishNotation 为 当前式子 的 （改良）后缀表达式 && 结果 && 字符串形式 的 数组
     */
    public String[] checkout(String formula,int length){
        // 操作数 && 操作符 && 逆波兰表达式
        Stack<String> stackNumber = new Stack<>();
        Stack<String> stackOperator = new Stack<>();
        String[] reversePolishNotation = new String[length];
        // 哈希表 存放运算符优先级
        HashMap<String, Integer> hashmap = new HashMap<>();
        hashmap.put("(", 0);
        hashmap.put("＋", 1);
        hashmap.put("－", 1);
        hashmap.put("×", 2);
        hashmap.put("÷", 2);

        for (int i=0,j=0; i < formula.length();) {
            //StringBuffer类中的方法主要偏重于对于字符串的变化，例如追加、插入和删除等，这个也是StringBuffer和String类的主要区别。
            StringBuilder digit = new StringBuilder();
            //将 式子 切割为 c字符
            char c = formula.charAt(i);
            //若 c字符 为10进制数字,将 c字符 加入digit（可以将多位数一起储存为一个数）
            while (Character.isDigit(c)||c=='/'||c=='\'') {
                digit.append(c);
                i++;
                c = formula.charAt(i);
            }

            if (digit.length() == 0){ //当前digit里面已经无数字，即当前处理符号
                switch (c) {
                    //如果是“(”转化为字符串压入字符栈
                    case '(': {
                        stackOperator.push(String.valueOf(c));
                        break;
                    }
                    //遇到“)”了，则进行计算，因为“(”的优先级最高
                    case ')': {
                        //将 stackOperator 栈顶元素取到 operator
                        String operator = stackOperator.pop();
                        //当前符号栈里面还有 ＋ － × ÷时，取 操作数 并 运算
                        while (!stackOperator.isEmpty() && !operator.equals("(")) {
                            //取操作数a,b
                            String a = stackNumber.pop();
                            String b = stackNumber.pop();
                            //后缀表达式变形
                            reversePolishNotation[j++] = a;
                            reversePolishNotation[j++] = b;
                            reversePolishNotation[j++] = operator;
                            //计算
                            String ansString = calculate(b, a, operator);
                            //如果 结果 不满足 要求 则 return -1，该式子不满足条件
                            if(ansString == null)
                                return  null;
                            //将结果压入栈
                            stackNumber.push(ansString);
                            //符号指向下一个计算符号
                            operator = stackOperator.pop();
                        }
                        break;
                    }
                    //遇到了“=”，则计算最终结果
                    case '=': {
                        String operator;
                        //当前符号栈里面还有 ＋ － × ÷时，即还没有算完，取 操作数 并 运算
                        while (!stackOperator.isEmpty()) {
                            //取值 && 取操作数
                            operator = stackOperator.pop();
                            String a = stackNumber.pop();
                            String b = stackNumber.pop();
                            //后缀表达式变形
                            reversePolishNotation[j++] = a;
                            reversePolishNotation[j++] = b;
                            reversePolishNotation[j++] = operator;
                            //计算
                            String ansString = calculate(b, a, operator);
                            if(ansString == null)
                                return null;
                            stackNumber.push(ansString);
                        }
                        break;
                    }
                    //不满足之前的任何情况
                    default: {
                        String operator;
                        //当前符号栈里面还有 ＋ － × ÷时，取 操作数 并 运算
                        while (!stackOperator.isEmpty()) {
                            //当前符号栈，栈顶元素
                            operator = stackOperator.pop();
                            if (hashmap.get(operator) >= hashmap.get(String.valueOf(c))) { //比较优先级
                                //取值
                                String a = stackNumber.pop();
                                String b = stackNumber.pop();
                                //后缀表达式变形
                                reversePolishNotation[j++] = a;
                                reversePolishNotation[j++] = b;
                                reversePolishNotation[j++] = operator;
                                //计算
                                String ansString =calculate(b, a, operator);
                                if(ansString == null)
                                    return  null;
                                stackNumber.push(ansString);
                            }
                            else {
                                stackOperator.push(operator);
                                break;
                            }

                        }
                        stackOperator.push(String.valueOf(c));  //将符号压入符号栈
                        break;
                    }
                }
            }
            //处理数字，直接压栈
            else {
                stackNumber.push(digit.toString());
                //reversePolishNotation[j++] = digit.toString();
                continue; //结束本次循环，回到for语句进行下一次循环，即不执行i++(因为此时i已经指向符号了)
            }
            i++;
        }
        //获取 栈顶数字 即 等式的最终答案
        reversePolishNotation[length-3] = "=";
        reversePolishNotation[length-2] = stackNumber.peek();
        reversePolishNotation[length-1] = formula;
        return reversePolishNotation;
    }

    /**
     * 计算式子运算结果
     * @param m 为 操作数
     * @param n 为 操作数
     * @param operator 为 运算符
     * @return ansFormula 为 当前式子 的 计算结果，若ansFormula为null，则不符合条件
     */
    private String calculate(String m,String n,String operator) {
        String ansFormula = null;//计算结果
        char op = operator.charAt(0);//符号
        int[] indexFraction = {m.indexOf('\''), m.indexOf('/'), n.indexOf('\''), n.indexOf('/')};//分数 各部分 切割位置

        //处理 含分数 的 运算
        if (indexFraction[1] > 0 || indexFraction[3] > 0) {
            int[] denominator = new int[3];
            int[] molecule = new int[3];
            int[] integralPart = new int[3];

            //切割分数
            if (indexFraction[1] > 0) {
                for (int i = 0; i < m.length(); i++) {
                    if (i < indexFraction[0]) {
                        integralPart[0] = Integer.parseInt(integralPart[0] + String.valueOf(m.charAt(i) - '0'));
                    } else if (i > indexFraction[0] && i < indexFraction[1]) {
                        molecule[0] = Integer.parseInt(molecule[0] + String.valueOf(m.charAt(i) - '0'));
                    } else if (i > indexFraction[1]) {
                        denominator[0] = Integer.parseInt(denominator[0] + String.valueOf(m.charAt(i) - '0'));
                    }
                }
            } else {
                integralPart[0] = Integer.parseInt(m);
                denominator[0] = 1;
                molecule[0] = 0;
            }

            if (indexFraction[3] > 0) {
                for (int i = 0; i < n.length(); i++) {
                    if (i < indexFraction[2]) {
                        integralPart[1] = Integer.parseInt(integralPart[1] + String.valueOf(n.charAt(i) - '0'));
                    } else if (i > indexFraction[2] && i < indexFraction[3]) {
                        molecule[1] = Integer.parseInt(molecule[1] + String.valueOf(n.charAt(i) - '0'));
                    } else if (i > indexFraction[3]) {
                        denominator[1] = denominator[1] + n.charAt(i) - '0';
                    }
                }
            } else {
                integralPart[1] = Integer.parseInt(n);
                denominator[1] = 1;
                molecule[1] = 0;
            }

            //分数运算
            switch (op) {
                case '＋': {
                    denominator[2] = denominator[0] * denominator[1];
                    molecule[2] = integralPart[0] * denominator[2] + molecule[0] * denominator[1]
                            + integralPart[1] * denominator[2] + molecule[1] * denominator[0];
                    break;
        }
                case '－': {
                    denominator[2] = denominator[0] * denominator[1];
                    molecule[2] = integralPart[0] * denominator[2] + molecule[0] * denominator[1]
                            - integralPart[1] * denominator[2] - molecule[1] * denominator[0];
                    break;
                }
                default:
                    return null;
            }

            //提取整数部分
            if (molecule[2] >= denominator[2] && molecule[2]>0) {
                integralPart[2] = molecule[2] / denominator[2];
                molecule[2] = Math.abs(molecule[2] % denominator[2]);
            } else if (molecule[2]<0) {
                return null;
            }

            //化简分数
            if (molecule[2] != 0) {
                ansFormula = greatFraction(integralPart[2],molecule[2],denominator[2]);
            } else ansFormula = String.valueOf(integralPart[2]);

        } else { //处理整数运算
            int a = Integer.parseInt(m);
            int b = Integer.parseInt(n);

            switch (op) {
                case '＋': {
                    ansFormula = String.valueOf(a + b);
                    break;
                }
                case '－': {
                    if (a - b >= 0)
                        ansFormula = String.valueOf(a - b);
                    else
                        return null;
                    break;
                }
                case '×': {
                    ansFormula = String.valueOf(a * b);
                    break;
                }
                case '÷': {
                    if (b == 0) {
                        return null;
                    } else if (a % b != 0) {
                        ansFormula = a % b + "/" + b;
                        if (a / b > 0) ansFormula = a / b + "'" + ansFormula;
                    } else
                        ansFormula = String.valueOf(a / b);
                    break;
                }
            }
        }
        return ansFormula;
    }

    /**
     * 化简分数
     * @param integralPart 为 分数的整数部分
     * @param molecule 为 分数的分子部分
     * @param denominator 为 分数的分母部分
     * @return ansFormula 为 当前式子 的 最简分数表达形式
     */
    private String greatFraction (int integralPart,int molecule,int denominator) {
        String ansFormula;
        int commonFactor = 1;

        //求最大公约数
        Create create = new Create();
        commonFactor = create.commonFactor(denominator,molecule);

        //化简分数
        denominator /= commonFactor;
        molecule /= commonFactor;

        //带分数 表示
        if (integralPart == 0 && molecule > 0) {
            ansFormula = String.valueOf(molecule) + '/' + String.valueOf(denominator);
        } else if (molecule == 0)
            ansFormula = String.valueOf(integralPart);
        else {
            ansFormula = String.valueOf(integralPart) + "'" + String.valueOf(molecule) + '/' + String.valueOf(denominator);
        }

        //返回最简分数
        return ansFormula;
    }

}

creat类

package fourcalculations;

import java.util.Random;

public class Create {
	 /**
     * 式子生成器
     * totalOperator 为 当前式子 的 运算符 数组
     * formula 为 当前式子 的 字符串形式
     * totalFraction 为 当前式子 的 操作数 数组
     * @param r 为 操作数 的 范围
     * @return ansFormula 为 当前式子 的 （改良）后缀表达式 && 结果 && 字符串形式 的 数组
     */
    public String[] createFormula(int r){
        Random random = new Random();
        String[] operator = {"＋","－","×","÷","＝"};

        //运算符 && 操作数 && 式子
        String[] totalOperator = new String[1 + random.nextInt(3)];
        String[] totalFraction = new String[totalOperator.length+1];
        String formula = new String();
        //是否包含分数
        Boolean hasFraction = false;

        //随机产生 操作数：
        for (int i=0;i<totalFraction.length;i++) {

            // 随机确定生成 整数 或 分数
            int fractionOrNot = random.nextInt(2);
            //生成
            if (fractionOrNot == 0) { //生成整数
                int integralPart = random.nextInt(r+1);
                totalFraction[i] = String.valueOf(integralPart);
            } else { //生成分数
                int denominator = 1+random.nextInt(r);
                int molecule = random.nextInt(denominator);
                int integralPart = random.nextInt(r+1);

                //化简分数
                if (molecule!=0) {
                    int commonFactor = commonFactor(denominator, molecule);
                    denominator /= commonFactor;
                    molecule /= commonFactor;
                }

                //输出最简分数
                if (integralPart == 0 && molecule > 0) {
                    totalFraction[i] = molecule + "/" + denominator;
                    hasFraction = true;
                }
                else if (molecule == 0)
                    totalFraction[i] = String.valueOf(integralPart);
                else {
                    totalFraction[i] = integralPart + "'" + molecule + "/" + denominator;
                    hasFraction = true;
                }
            }
        }

        //随机生成 运算符：
        for (int i=0;i < totalOperator.length;i++) {
            if (hasFraction)
                totalOperator[i] = operator[random.nextInt(2)];
            else
                totalOperator[i] = operator[random.nextInt(4)];
        }

        //随机选择式子括号起始位置；当式子形如 a+b= 时，不加括号
        int choose = totalFraction.length;
        if (totalFraction.length != 2 )
            choose = random.nextInt(totalFraction.length);

        //合成式子 formula
        for (int i=0;i<totalFraction.length;i++) {
            if (i == choose && choose<totalOperator.length) {
                formula = formula + "(" + totalFraction[i] + totalOperator[i] ;
            } else if (i == totalFraction.length - 1 && i == choose+1 && choose<totalOperator.length) {
                formula = formula + totalFraction[i] + ")" + "=";
            } else if (i == choose+1 && choose<totalOperator.length) {
                formula = formula + totalFraction[i] + ")" + totalOperator[i];
            } else if (i == totalFraction.length - 1) {
                formula = formula + totalFraction[i] + "=";
            } else {
                formula = formula + totalFraction[i] + totalOperator[i];
            }
        }

        //检查运算结果
        CheckAnswer checkAns = new CheckAnswer();
        String[] ansFormula = checkAns.checkout(formula,3*totalOperator.length+2+1);//2*totalOperator.length+3+1

        //System.out.println("ansFormula："+Arrays.toString(ansFormula));
        if (ansFormula!=null)
            return ansFormula;
        return null;
    }

    /**
     * 求最大公因数，以化简分数
     * @param x 为 操作数 的 分母
     * @param y 为 操作数 的 分子
     * @return y 为 最大公因数
     */
    public int commonFactor(int x,int y) {
        while(true)
        {
            if(x%y==0)return y;
            int temp=y;
            y=x%y;
            x=temp;
        }
    }
}




