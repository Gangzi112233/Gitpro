package xmbb;

import java.util.Scanner;

public class Demo {

	// 加密第一步，将字符串的每个字符转化为ASCII值并进行加值操作
	public static char[] encryptFirst(char[] nums) {

		for (int i = 0; i < nums.length; i++) {
			int j = (int) nums[i];// 每个字符转化为ASCII值
			int j1 = j + i + 1 + 3;// 将转化之后的值加上在字符串中的位置和3
			if (j1 > 127) {
				j1 -= 127;
			}
			nums[i] = (char) j1;
		}
		return nums;
	}

//解密的第一步，将字符串的每个字符转化为ASCII值并进行减值操作
	public static char[] encryptFirst1(char[] nums) {

		for (int i = 0; i < nums.length; i++) {
			int j = (int) nums[i];// 每个字符转化为ASCII值
			int j1 = j - i - 1 - 3;// 将转化之后的值加上在字符串中的位置和3
			if (j1 < 0) {
				j1 += 127;
			}
			nums[i] = (char) j1;
		}
		return nums;
	}

	// 加密第二步，将字符数组中的首尾进行调换
	public static char[] encryptSecond(char[] nums2) {
		char i = ' ';
		int length = nums2.length;
		i = nums2[0];
		nums2[0] = nums2[length - 1];
		nums2[length - 1] = i;
		return nums2;
	}

	public static boolean judgeNum(char[] nums3) {
		boolean flag = true;
		for (char i : nums3) {
			if (!((int) i >= 48 && (int) i <= 57)) {
				flag = false;
			}
		}
		return flag;
	}

	public static boolean judgeChar(char[] nums4) {
		boolean flag = true;
		for (char i : nums4) {
			if (!((int) i >= 65 && (int) i <= 122)) {
				flag = false;
			}
		}
		return flag;
	}

	public static boolean judgeNum1(char[] nums4) {
		for (char i : nums4) {
			if (((int) i >= 48 && (int) i <= 57)) {
				return true;
			}
		}
		return false;
	}

	public static boolean judgeChar1(char[] nums4) {
		for (char i : nums4) {
			if (((int) i >= 65 && (int) i <= 122)) {
				return true;
			}
		}
		return false;
	}

	public static boolean judgeBChar(char[] nums4) {
		for (char i : nums4) {
			if (((int) i >= 65 && (int) i <= 90)) {
				return true;
			}
		}
		return false;
	}

	public static boolean judgeSChar(char[] nums4) {
		for (char i : nums4) {
			if (((int) i >= 97 && (int) i <= 122)) {
				return true;
			}
		}
		return false;

	}
	
	 private static void checkPasswordStrength(String password) {
	        if (password.length() < 8 || password.length() >= 8 && password.matches("[0-9]+") || password.matches("[a-zA-Z]+")) {
	            System.out.println("弱强度密码");
	        } else if (password.length() >= 8 && password.matches(".*\\d.*") && password.matches(".*[a-zA-Z].*")) {
	            System.out.println("中强度密码");
	        } else if (password.length() >= 8 && password.matches(".*\\d.*") && password.matches(".*[a-z].*") && password.matches(".*[A-Z].*")) {
	            System.out.println("高强度密码");
	        }
	    }
	 
	 private static String generatePassword(int length) {
	        StringBuilder password = new StringBuilder();
	        for (int i = 0; i < length; i++) {
	            char randomChar = (char) ('0' + (Math.random() * 36));
	            password.append(randomChar);
	        }   return password.toString();
	    }
	        
	public static void menu() {
		System.out.println("===========================");
		System.out.println("      欢迎使用密码管理系统     ");
		System.out.println("===========================");
		System.out.println("         请选择操作:         ");
		System.out.println("     1.加密     2.解密      ");
		System.out.println("       3.判断密码强度        ");
		System.out.println("     4.密码生成  5.退出      ");
	}

	public static void  main(String[] args) {

        int input=0;
        do{
            menu();
            
            Scanner scanner=new Scanner(System.in);
            System.out.print("请输入");
            input=new Scanner(System.in).nextInt();
            switch (input){
                case 1: System.out.println("===========================");
                        System.out.println("      欢迎使用密码管理系统     ");
                        System.out.println("===========================");
                        System.out.print("请输入要加密的数字密码:");
                        Scanner scanner1=new Scanner(System.in);
                        String s = scanner1.nextLine();
                        char[] chars1 = encryptSecond(encryptFirst( s.toCharArray()));
                        String s2 = String.valueOf(chars1);
                        StringBuffer stringBuffer=new StringBuffer(s2);
                        String s3 = stringBuffer.reverse().toString();
                        System.out.println("加密后的结果是:"+s3);
                        break;

                case 2: System.out.println("===========================");
                        System.out.println("      欢迎使用密码管理系统     ");
                        System.out.println("===========================");
                        System.out.print("请输入要解密的数字密码:");
                        Scanner scanner2=new Scanner(System.in);
                        String s1 = scanner2.nextLine();
                        StringBuffer stringBuffer1=new StringBuffer(s1);
                        String s4 = stringBuffer1.reverse().toString();
                        char[] chars = encryptSecond(s4.toCharArray());
                        char[] chars2 = encryptFirst1(chars);
                        String s5 = String.valueOf(chars2);
                        System.out.println("解密后的结果是:"+s5);
                        break;
                     
                case 3:
                       System.out.print("请输入需要判断强度的密码： ");
                       String passwordToCheck = new Scanner(System.in).nextLine();
                       checkPasswordStrength(passwordToCheck);
                       break;
              
                case 4:
                       System.out.print("请输入生成密码的长度： ");
                       int passwordLength = new Scanner(System.in).nextInt();
                       String generatedPassword = generatePassword(passwordLength);
                       System.out.println("生成的密码: " + generatedPassword);
                       break;
                case 0:
                       System.out.println("退出密码管理系统。");
                       System.exit(0);
                default:
                       System.out.println("无效的选项，请重新输入。");
            }      

        }while(input!=5);
        
        }
	
	}
