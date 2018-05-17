package pers.li.io;

import java.io.File;
import java.io.FilenameFilter;

public class FileTest {

    public static void main(String[] args) throws Exception{

        File file=new File(".");
        System.out.println("文件名称："+file.getName());
        System.out.println("获取相对路径的父路径：错误"+file.getParent());
        System.out.println("获取绝对路径："+file.getAbsolutePath());
        System.out.println("获取绝对路径："+file.getAbsoluteFile());
        System.out.println("获取上一级路径："+file.getAbsoluteFile().getParent());

        //在file路径下创建临时文件
        File tem =File.createTempFile("aaa",".txt",file);
        //指定jvm退出时删除该文件
        tem.deleteOnExit();

        File newFile=new File(System.currentTimeMillis()+"");
        System.out.println("newFile文件是否存在："+newFile.exists());
        newFile.createNewFile();
        boolean rename = newFile.renameTo(new File("rename"));
        System.out.println("重命名是否成功："+rename);
        System.out.println("createNewFile后newFile文件是否存在："+newFile.exists());
        boolean mkdir = newFile.mkdir();
        System.out.println("createNewFile后mkdir是否成功："+mkdir);
        String [] list=file.list();
        for (String filename:list
             ) {
            System.out.println("打印出当前工程下所有的filename："+filename);
        }
        System.out.println("以上打印不包含使用deleteOnExit方法的文件，因为JVM退出被删除");
        File [] roots=File.listRoots();
        //列出所有磁盘根路径
        for (File f:roots
             ) {
            System.out.println(f);//C:\
        }
        newFile.delete();

        System.out.println("--------文件过滤器---------------------------------");
        String [] nameList=file.list(new FilenameFilter() {
            @Override
            public boolean accept(File dir, String name) {
                boolean b = name.endsWith(".java");
//                boolean directory = new File(name).isDirectory();
                return b;
            }
        } );
        for (String name:
            nameList ) {
            System.out.println(name);
        }

    }

}
