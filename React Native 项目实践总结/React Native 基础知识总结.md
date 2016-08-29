##React Native �ܽ�



###Component
Component�������ʹ��```extends React.Component```��������Ϊ�����?
 ```componentWillMount()```��������``` constructor ```�����棺

	class Label extends React.Component{
	  constructor(props) {
          super(props);  
      }
	    render(){
	    }
	}


###props��state

#####props���ԣ�
������Զ����ʼֵ���Լ����ɸ���props����ֵ��ֻ����Ӹ�����д��ݹ�����

	// �����
	class ParentComponent extends React.Component{
	    render(){
	        return(<Child name="name">);
	    }
	}
	
	// �����
	class Child extends React.Component{
	    render(){
	        return(<Text>{this.props.name}</Text>);
	    }
	}
	
����������������name="name"��props���ԣ����������ʹ��this.props.name���ô����ԡ�

��������``` prop type ```��Ĭ������ ```default prop ```����ͨ�����е� ```static ```��������

	class Demo extends React.Component {
	   // Ĭ��props
	  static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
	  }
  	   // propTypes������֤ת���props������ props ������Ч����ʱ��JavaScript ����̨���׳�����
	  static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
	  }
	  state = {
        loopsRemaining: this.props.maxLoops,
	  }
	}
#####state���ԣ�
��������ı��Լ�״̬�����ԣ�ͨ��ʹ��```setState({key:value})```���ı�����ֵ��������ˢ�£�����ʹ��```this.state.xxx```��ֱ�Ӹı䡣
�ڿ����У�һ�㲻���ڶ�ʱ��������setInterval��setTimeout�ȣ���������state�����͵ĳ������ڽ��յ����������ص������ݣ��������û���������֮��

���ھ����ı����������Ҫˢ�½�����ʾ������ʹ��state�����ڲ���Ҫ�ı������ֵ����ʹ��props��React Native�����ɶ���ĸ��������stateֵ������stateֵ��Ϊ�������props����ֵ���ݸ���������������Ա��ֵ�һ�����ݴ��ݡ�


	
###��������

���ǰ������```װ��```����```��Ⱦ```���ٵ�```ж��```����һ���������ڣ�Ҳ�������������״̬��```װ��```��ʼ��```ж��```Ϊֹ���ڼ���Ը������Եı仯���ж����Ⱦ��
�������ڵ�����״̬��
-	Mounting��װ��
1.componentWillMount()
2.componentDidMount()
-	Updating����Ⱦ
1.componentWillReceiveProps()
2.shouldComponentUpdate()
3.componentWillUpdate()
4.componentDidUpdate()
-	Unmounting��ж��
componentWillUnmount()

```
componentWillMount()�������ʼװ��֮ǰ���ã���һ������������ֻ��ִ��һ�Ρ�

componentDidMount()��������װ��֮���������ã���һ������������ֻ��ִ��һ�Ρ������￪ʼ�Ϳ��Զ�������и��ֲ����ˣ����������װ����ɺ�Ҫ��ʾ��ʱ��ִ�ж�����


componentWillUpdate(object nextProps, object nextState)�����µ�props����state������ʱ,������Ը���֮ǰ����,����������ᱻ��ʼ��Ⱦ���á����������������ʹ�� this.setState()�������Ҫ��Ӧһ��prop�仯������state,ʹ��componentWillReceiveProps �������

componentDidUpdate(object prevProps, object prevState)��������Ը���֮����ã�ÿ�����Ը��¶�����ã�����������ᱻ��ʼ��Ⱦ���á�

componentWillUnmount()�����ж��֮ǰ���ã������������ִ��һЩ��Ҫ���������,����timers��
```

#####������Ը���ʱ��������·�������һ�����������п���ִ�ж�Σ�

	componentWillReceiveProps(object nextProps)���Ѽ�������յ��µ�propsʱ������.�����������Ϊ�������Ⱦ���á�
	
	shouldComponentUpdate(object nextProps, object nextState)������ж��Ƿ�������Ⱦʱ���ã����µ�props����state���յ�,����Ⱦǰ������.��������������������Ⱦ�����á�
	
��û�����Ƶ� ```componentWillReceiveState ()```�ķ�����һ������������ prop ת����ܻᵼ��һ�� state �仯,���Ƿ�֮���ǡ��������Ҫʵ��һ���� state �仯��Ӧ�Ĳ�����ʹ�� ```componentWillUpdate()```��


��� shouldComponentUpdate () ����false, render() �����´�state�仯ǰ����ȫ����������componentWillUpdate () �� componentDidUpdate()  �����ᱻ���á�

Ĭ�������shouldComponentUpdate()  ���Ƿ��� true ����ֹ�� state ͻ��ʱ��ϸ΢bug��
	
	
###ҳ����ת

��ʼ����һ��ҳ�棺

	import SeatPageComponent from './SeatPageComponent';
	import MainPageComponent from './MainPageComponent';
	import TrainListComponent from './TrainListComponent';
	
	class MainPage extends React.Component {
	    render() {
	        let defaultName = 'MainPageComponent';
	        let defaultComponent = MainPageComponent;
	        return (
	            <Navigator
	                // ָ��Ĭ��ҳ��
	                initialRoute={{ name: defaultName, component: defaultComponent }}
	                // ����ҳ�����ת����
	                configureScene={(route) => {
	                    return Navigator.SceneConfigs.VerticalDownSwipeJump;
	                }}
	                // ��ʼ��Ĭ��ҳ��
	                renderScene={(route, navigator) => {
	                    let Component = route.component;
	                    // ��navigator��Ϊprops���ݵ���һ��ҳ��
	                    return <Component {...route.params} navigator={navigator} />
	                }} />
	        );
	    }
	}
	

��ת����һҳ�棺

	jumpToNext(){
	      const { navigator } = this.props;// ����һ��ҳ�洫�ݹ���
	      if(navigator) {
	          navigator.push({
	              name: 'SeatPageComponent',
	              component: SeatPageComponent,// ��һ��ҳ��
	          });
	      }
	}

������һ��ҳ�棺

	 _back(){
	     const { navigator } = this.props;
	     if(navigator) {
	         navigator.pop();
	     }
	 }
	
ҳ���ͨ��

���磺��Aҳ���Bҳ��
Aͨ��route.params���������ݸ�B��

	jumpToNext(){ 
	    const { navigator } = this.props;// ����һ��ҳ�洫�ݹ���
	    if(navigator) { 
	        navigator.push({ 
	            name: 'SeatPageComponent', 
	            component: SeatPageComponent,// ��һ��ҳ�� 
	            params: { // ��Ҫ���ݸ���һ��ҳ��Ĳ���,�ڶ���ҳ��ʹ��this.props.xxx��ȡ����
	                id: 123,
	                title: this.state.title, 
	            },
	        });
	     }
	}
	
Aͨ��route.params���ݻص���������A����������B�����ݴ��ظ�A��

	// Aҳ��
	jumpToNext(){ 
	    const { navigator } = this.props;// ����һ��ҳ�洫�ݹ���
	    if(navigator) { 
	        let that = this;// this�����򣬲μ����ĺ�����
	        navigator.push({ 
	            name: 'SeatPageComponent', 
	            component: SeatPageComponent,// ��һ��ҳ�� 
	            params: { // ��Ҫ���ݸ���һ��ҳ��Ĳ���,�ڶ���ҳ��ʹ��this.props.xxx��ȡ����
	                title: '����',
	                getName: function(name) {that.setState({ name: name })}
	            },
	        });
	     }
	}
	
	// Bҳ��
	 _back(){
	     const { navigator } = this.props;
	     if(this.props.getName){
	         this.props.getName('����');
	     }
	     if(navigator) {
	         navigator.pop();
	     }
	 }



###flexbox����
#####ʲô��flexbox����
React��������flexbox����,flexbox������webǰ������CSS��һ�ֲ��ַ�������2009��W3C�����һ���µĲ��ַ��������Լ�㡢��������Ӧʽ��ʵ�ָ���ҳ�沼�֡�
RN����flexBoxģ�Ͳ���, Ҳ�������ֻ���Ļ�϶������������.����flexBoxģ��,�����߿��Կ�������̬��ߵ�����Ӧ��UI���֡�

#####flexbox�е���ʽ��Ҫ�����¼���:
1.	λ�ü�������ص���ʽ��
2.	��������,������������й���ļ�
3.	Ԫ������,���������ʾ����ļ�
4.	�߿򡢿�϶�����

#####������ʽ 
- position
 ```relative```(Ĭ��) ��ʾ��ǰ������λ������Զ�λ��������ʹ��``` bottom```��```right```��```top```��```left```��ʾ��ǰ���������һ��ͬ�����������(��)����
 ```absolute``` ��ʾ��ǰ������λ���Ǿ��Զ�λ��``` top``` ��```bottom```��``` left```�� ```right```��������ǰ�����λ�þ��븸�������¡�����)�ľ���
- width
 ```width```��```height```��```maxHeight```��```maxWidth```��```minHeight```��```minWidth``` ����Ŀ�͸��ǿ��Զ�̬�ı��,���Կ������ÿ�͸ߵ�������Сֵ 
- flexDirection
 ```row```���������У�<b>����</b>Ϊˮƽ����
 ```?column```����ֱ���У�<b>����</b>Ϊ��ֱ���� 
- flexWrap
 ```?wrap ```?�� ```?nowrap ```?(Ĭ��ֵ)?����ˮƽ��ֱ����ʱ�������View�Ų��¿�ѡ ```?wrap ```?ʵ���Զ�����,
- justifyContent 
�Ӳ��������᷽��λ��  enum(```flex- start```,```flex-end```,```center```,```space-between```,```space-around```)
- alignItems
  �Ӳ����ڲ��᷽��λ�� enum(```flex-start```,```flex-end```,```center```,```stretch``` )
- flex
 Ȩ�أ�Ĭ��ֵ��0������ֵΪ1ʱ����������Զ���������Ӧ�����ʣ�µĿհ׿ռ䡣
- alignSelf
 �������ĸ������ʽ�е�```alignItems```��ȡֵ�����Ը����ʹ��```alignSelf```����Ӧ�Ĺ���
enum(```auto```,```flex-start```,```flex-end```,```center```,```stretch```)
- padding
- margin


![����ģ��ʾ��ͼ](http://upload-images.jianshu.io/upload_images/1132780-3e6d1a45fb4550ce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


