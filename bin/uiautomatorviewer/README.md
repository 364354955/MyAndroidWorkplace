# �Զ���uiautomatorviewer xpath����
* ��ʹ���Զ�����������Ҫ��λԪ��.һ�㶼��ʹ��sdk�����uiautomatorviewer,���˹���ֻ�ܶ�λid,class,name�ȣ�����û��xpath
* [��������](https://android.googlesource.com/platform/frameworks/uiautomator/+/android-sdk-4.4.2_r1.0.1) - `Դ������uiautomatorviewer`
* ��Ҫ�������ļ�
	* ��Ӧ��android.jar
	* com.google.guava_XXX.jar
	* common.jar
	* ddmlib.jar
	* org.eclipse.core.commands_XXX.jar
	* org.eclipse.equinox.common_XXX.jar
	* org.eclipse.jface_XXX.jar
	* org.eclipse.swt.XXX.jar
	
* org.eclipse.jdt.core.prefs ����������ļ�Ҫע���£���ʱ��ᱨ��java�ı���汾���󣬴˿ӿӵ���̫��

* com.android.uiautomator:���uiautomatorviewer���ߵ�GUI������룬���������UiAutomatorViewer.java�ļ�������main������ڣ����ߵĴ��ھ��ڴ˴�����
* com.android.uiautomator.actions���������anction�������磺Device screenshot ��open�ȡ�
* com.android.uiautomator.tree�����tree��װ��dump������xml������һ��������tree��������Ǻ��İ���

## �����޸Ĳ���
### com.android.uiautomator.tree
#### UiNode.class
```
// �ҵ�����
    private String getNodeClassAttribute() {
  		return this.mAttributes.get("class");
  	}
	
	  //�ҵ�����
    public String getXpath()
    {
        String className=getNodeClassAttribute();
        String xpath="//"+className;
        String text = getAttribute("text");
        if(text !=null&& !text.equals(""))
        {
            xpath += "[@text='"+text+"']";
            return xpath;
        }else 
        {
            return getAttribute("content-desc") !=""?
                    xpath+"[@content-desc='"+getAttribute("content-desc")+"']"
                    :xpath+"[@index='"+getAttribute("index")+"']";
        }

    }
```

#### UiHierarchyXmlLoader.calss
```
//�ҵ�����
    private UiNode mTmpNode ;
	public BasicTreeNode parseXml(String xmlPath) {
                    //�ҵ��޸�
                    if (mParentNode != null) {
                        mParentNode.addChild(mWorkingNode);
                        //System.out.println(mNodeList.size());
                        if(mWorkingNode.getParent()!=null){
                        	String xpath = ((UiNode)mWorkingNode).getXpath();
                        	((UiNode)mWorkingNode).addAtrribute("xpath",xpath);
                        }
                        mNodeList.add(mWorkingNode);

                        //System.out.println(mNodeList.size());
                    }
```



![pic.png](pic.png "pic.png")
