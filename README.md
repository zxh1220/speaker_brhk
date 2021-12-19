# speaker_brhk
博瑞云音箱云喇叭自定义播报内容免费API接口

<p style="margin-left:0; margin-right:0; text-align:center"><span>&nbsp;</span><span>&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span>&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:center"><img alt=""  src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bad7c7c28db34f49b9e04c6d33602ec7~tplv-k3u1fbpfcp-zoom-1.image" width="1194" /></p>

<p style="margin-left:0; margin-right:0">&nbsp;</p>

<h1><span style="color:#262626">云音箱服务对接指南</span></h1>

<p style="margin-left:0; margin-right:0; text-align:center"><span style="color:#262626">&nbsp;</span><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:center"><span style="color:#f5222d">&nbsp;</span><span>（流量版喇叭对接，可以只看3.1小节）</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h1><span>一、名词解释&nbsp;</span><span style="color:#8c8c8c">(</span><span style="color:#f5222d">开发前必读</span><span style="color:#8c8c8c">)</span></h1>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h3><span>1、云音箱&nbsp;ID&nbsp;(SPEAKERID、sn)：&nbsp;喇叭标签上的SN码</span></h3>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">云音箱机身上帖有云音箱的&nbsp;ID&nbsp;码，每台云音箱拥有唯一永久&nbsp;ID，SPEAKERID由字母、数字组成， 在生产过程中写入云音箱，云音箱出厂后不会再改变。</span><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h3><span>2、TOKEN (接口凭证)：&nbsp;</span><span style="color:#f5222d">必须</span></h3>

<p style="margin-left:0; margin-right:0; text-align:justify"><span>程序调用接口控制音箱播报的凭证，</span><span style="color:black">预先</span><strong><span style="color:black">联系客服</span></strong><span style="color:black">申请分配，使得程序对该 SPEAKERID&nbsp;有操控权限。只要设备授权给TOKEN，一个TOKEN可以控制无数个设备。</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h3><span>3、version（接口版本）：(</span><span style="color:#f5222d">非常重要</span><span>)</span></h3>

<p style="margin-left:0; margin-right:0; text-align:justify"><strong><span style="color:#08979c">由于喇叭硬件的变动，可能带来接口的变动，用此参数区分，要求开发者后台预留（1-9）个版本选项，</span></strong><strong><span style="color:#e8323c">喇叭机身的标签中</span></strong><strong><span style="color:#08979c">，会注明对应的</span></strong><strong><span style="color:#ff4d4f">version</span></strong></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#ff4d4f">比如 </span></strong></p>

<p style="margin-left:0; margin-right:0"><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dd7642925dcb4bc8a71d1d21f4c66af5~tplv-k3u1fbpfcp-zoom-1.image" width="960" /></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:35px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>型号</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:35px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>VERSION/接口版本</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:35px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>型号</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:35px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>VERSION/接口版本</span></strong></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>210/</span></strong><strong><span style="color:#f5222d">310</span></strong><strong><span>/330</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>1</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span style="color:#f5222d">402</span></strong><strong><span>/</span></strong><strong><span style="color:#389e0d">404</span></strong><strong><span>/</span></strong><strong><span style="color:#c41d7f">502</span></strong><strong><span>/</span></strong><strong><span style="color:#061178">504</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>3</span></strong></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>204</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>2</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span style="color:#1890ff">901/902</span></strong></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0; text-align:center"><strong><span>9</span></strong></p>
			</td>
		</tr>
	</tbody>
</table>

<h1><span>二、接口&nbsp;</span></h1>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h2><span>1</span><span>、通讯协议</span><span style="color:#8c8c8c">（作为了解）</span></h2>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h4><span>1）接口网关：</span></h4>

<p style="margin-left:0; margin-right:0"><a href="https://speaker.17laimai.cn" target="_blank"><span>https://speaker.17laimai.cn</span></a><span>&nbsp;</span></p>

<h4><span>2）协议和端口号：</span></h4>

<p style="margin-left:0; margin-right:0"><span>&nbsp;HTTP 80，</span><strong><span>HTTPS 443</span></strong><span> &nbsp;</span></p>

<h4><span>3）请求方式：GET&nbsp;或&nbsp;POST (</span><span style="color:#ff7a45">推荐使用POST,数据更安全</span><span>)&nbsp;</span></h4>

<h4><span>4）提交数据格式：</span></h4>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">id=SPEAKERID&amp;uid=USERID&amp;price=PRICEVALUE&amp;token=TOKEN&amp;version=1</span></p>

<h4><span>5）返回数据格式：JSON</span></h4>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">类型</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errcode</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">integer</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回码</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errmsg</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">返回码描述</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">detail</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回的数据</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h4><span>6）网关返回码</span></h4>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:720px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">0&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">成功</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">1&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">未知错误</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">2&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SPEAKERID&nbsp;</span><span style="color:black">不存在</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">3&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SPEAKERID&nbsp;</span><span style="color:black">已经被其它用户</span><span style="color:black">&nbsp;ID&nbsp;</span><span style="color:black">绑定</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">4&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SPEAKERID&nbsp;</span><span style="color:black">已经被同一用户</span><span style="color:black">&nbsp;ID&nbsp;</span><span style="color:black">绑定</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">5&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SPEAKERID&nbsp;</span><span style="color:black">未被任何用户</span><span style="color:black">&nbsp;ID&nbsp;</span><span style="color:black">绑定</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">6&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">未提供</span><span style="color:black">&nbsp;SPEAKERID</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">8&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">此</span><span style="color:black">&nbsp;token&nbsp;</span><span style="color:black">无此</span><span style="color:black">&nbsp;SPEAKERID&nbsp;</span><span style="color:black">权限</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">9&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">无效的</span><span style="color:black">&nbsp;token</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">17&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">重复的请求</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">本文档接口表格中各列意义说明：</span><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#262626">&ldquo;</span><span style="color:#262626">参数</span><span style="color:#262626">&rdquo;</span><span style="color:#262626">列</span><span style="color:#262626">:&nbsp;</span><span style="color:#262626">指提交</span><span style="color:#262626">&nbsp;GET&nbsp;</span><span style="color:#262626">或</span><span style="color:#262626">&nbsp;POST&nbsp;</span><span style="color:#262626">方式时带的参数名称字符串，编程时使用</span></p>

<p style="margin-left:0; margin-right:0"><span>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#262626">&ldquo;</span><span style="color:#262626">意义</span><span style="color:#262626">&rdquo;</span><span style="color:#262626">列</span><span style="color:#262626">:&nbsp;</span><span style="color:#262626">解释参数名称的意义，仅为了利于记忆，不是编程时的字符串</span><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span>&middot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span><span style="color:#262626">&ldquo;</span><span style="color:#262626">必须</span><span style="color:#262626">&rdquo;</span><span style="color:#262626">列：带</span><span style="color:#262626">*</span><span style="color:#262626">号表示此参数是必须的，不能缺少</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:#262626">&nbsp;</span></p>

<h2><span>2</span><span>、基础接口</span></h2>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">基础接口为云音箱正常工作的必备接口，代理商必须实现</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<h3><span>2.1 </span><span>云音箱绑定或解绑</span><span style="color:#fa8c16">（WIFI版</span><span style="color:#f5222d">必</span><span style="color:#fa8c16">用，流量版</span><span style="color:#f5222d">选</span><span style="color:#fa8c16">用）</span></h3>

<p style="margin-left:0; margin-right:0"><strong><span style="background-color:#fcfcca; color:#e8323c">注意：310、330使用add播报方法时，必须先调用绑定方法进行绑定，其它型号可以不绑定；另外notify方法，全部型号可以不调用绑定方法，流量版推荐notify方法。</span></strong></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">1</span><span style="color:black">）</span><span style="color:black">URL: &nbsp;</span><a href="https://speaker.17laimai.cn/bind.php" target="_blank"><strong><span style="color:#262626">https://speaker.17laimai.cn/bind.php</span></strong></a></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">2</span><span style="color:black">）请求参数：</span></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:750px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">意义</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">id&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SPEAKERID&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">指该云音箱标签上的的&nbsp;SN/ID</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">m&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">METHOD&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">0&nbsp;</span><span style="color:black">为解绑，</span><span style="color:black">&nbsp;1&nbsp;</span><span style="color:black">为绑定</span><span style="color:black">,&nbsp;4&nbsp;</span><span style="color:black">强制解绑（不需提供原</span><span style="color:black">&nbsp;USERID</span><span style="color:black">）</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">uid&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">USERID&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#fa8c16">开发者自定义，保持在你自己的系统程序内唯一即可,如：商家手机号</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">token&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">TOKEN&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">代理商的</span><span style="color:black">&nbsp;token,&nbsp;</span><span style="color:black">预先通过安全渠道分配，使得代理商对该</span><span style="color:black"> SPEAKERID&nbsp;</span><span style="color:black">有操作权限</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="background-color:#ffffff; border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0"><span>version</span></p>
			</td>
			<td style="background-color:#ffffff; border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0"><span>接口版本</span></p>
			</td>
			<td style="background-color:#ffffff; border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0"><span style="color:#404040">按各型号标注的VERSION版本，由用户配置时选择，</span><strong><span style="color:#f5222d">预留1-9供选择</span></strong></p>
			</td>
			<td style="background-color:#ffffff; border-color:#d9d9d9; border-style:solid; border-width:1px; height:33px">
			<p style="margin-left:0; margin-right:0"><span>*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">seq&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">SEQUENCY&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">用</span><span style="color:black">&nbsp;</span><span style="color:black">于通讯</span><span style="color:black">&nbsp;</span><span style="color:black">去重复</span><span style="color:black">&nbsp;</span><span style="color:black">的顺序号</span><span style="color:black">&nbsp;</span><span style="color:black">，范围</span><span style="color:black">&nbsp;</span><span style="color:black">为</span><span style="color:black">&nbsp;[0,4294967295]&nbsp;(&nbsp;</span><span style="color:black">即</span><span style="color:black"> [0,0xFFFFFFFF])</span><span style="color:black">的整数。每次提交时请改变此值（比如按顺序</span><span style="color:black"> </span><span style="color:black">加</span><span style="color:black">&nbsp;1</span><span style="color:black">）。</span><span style="color:black"> </span><span style="color:black">假如服务器在</span><span style="color:black">&nbsp;200&nbsp;</span><span style="color:black">秒（暂定值）内收到两个或多个</span><span style="color:black">&nbsp;SEQUENCY</span><br />
			<span style="color:black">相同、并且提交的内容也相同的请求，则认为是重复提交，</span><span style="color:black"> </span><span style="color:black">将忽略此请求，并返回错误码</span><span style="color:black">&nbsp;17</span><span style="color:black">。</span><span style="color:black"> </span><span style="color:black">此参数缺省时，服务器对此次请求不做去重检查，此次请求</span><span style="color:black"> </span><span style="color:black">也不作为后续去重检查的比较依据。</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">descs&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">DESCRIPTION&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">代理商可以给此绑定请求提供一个描述字符串，最大</span><span style="color:black">&nbsp;255&nbsp;</span><span style="color:black">个</span><span style="color:black"> </span><span style="color:black">字节。之后代理商用</span><span style="color:black">&nbsp;&ldquo;&nbsp;</span><span style="color:black">绑定状态查询接口</span><span style="color:black">&rdquo;</span><span style="color:black">查询绑定消息时，</span><span style="color:black"> </span><span style="color:black">可以看到此描述。</span><span style="color:black"> </span><span style="color:black">此参数对云音箱或服务器工作状态没有影响。</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">例子</span><span style="color:black">1</span><span style="color:black">：</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#1890ff">https://speaker.17laimai.cn/bind.php?id=335&amp;m=1&amp;uid=AF337099&amp;token=123456789021</span><span style="color:#1890ff">&amp;version=1</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">表示申请将用户</span><span style="color:black">&nbsp;ID&nbsp;AF337099&nbsp;</span><span style="color:black">与云音箱</span><span style="color:black">&nbsp;335&nbsp;</span><span style="color:black">绑定</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">例子</span><span style="color:black">2</span><span style="color:black">：</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#1890ff">https://speaker.17laimai.cn/bind.php?id=335&amp;m=0&amp;uid=AF337099&amp;token=123456789021</span><span style="color:#1890ff">&amp;version=1</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">表示申请将用户</span><span style="color:black">&nbsp;ID&nbsp;AF337099&nbsp;</span><span style="color:black">与云音箱</span><span style="color:black">&nbsp;335&nbsp;</span><span style="color:black">解除绑定</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">3) </span><span style="color:black">返回参数：</span></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">类型</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errcode</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">integer</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回码，参见</span><span style="color:#262626"> </span><span>网关返回码</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errmsg</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">返回码描述</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">detail</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回的数据</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<h3><span>2.2 支付语音播报（WIFI\流量版</span><span style="color:#f5222d">通</span><span>用）</span></h3>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">将支付结果提交到云音箱服务器、服务器将支付结果推送给云音箱，云音箱接收后播报。</span></p>

<p style="margin-left:0; margin-right:0"><strong><span style="background-color:#fcfcca; color:#e8323c">&nbsp;注意：310、330使用此方法时，必须先调用绑定方法进行绑定，notify方法不需要，流量版推荐notify方法。</span></strong></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#262626">1</span></strong><strong><span style="color:#262626">）</span></strong><strong><span style="color:#262626">URL</span></strong><strong><span style="color:#262626">：</span></strong><a href="https://speaker.17laimai.cn/add.php" target="_blank"><strong><span style="color:#262626">https://speaker.17laimai.cn/add.php</span></strong></a><strong><span style="color:#f5222d">（WIFI版、流量版通用播报接口）</span></strong></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">2</span><span style="color:black">）请求参数：</span></p>

数：

| 参数                                                                                                                                                                             | 意义                                                                                                   | 解释                                                                                                                                                                                                     | 必须  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --- |
| id                                                                                                                                                                             | SPEAKERID                                                                                            | 指该云音箱标签上的的 SN/ID                                                                                                                                                                                       | *  |
| uid                                                                                                                                                                            | USERID                                                                                               | 开发者自定义，保持在你自己的系统程序内唯一即可,如：商家手机号                                                                                                                                                                        |     |
| price                                                                                                                                                                          | PRICEVALUE                                                                                           | 指支付金额值的字符串，单位为分，范围为 1 至 2147483647，即 1 分到 2 千多万。                                                                                                                                                       | *  |
| pt                                                                                                                                                                             | PRICE_TYPE                                                                                           | 支付类型，此参数会让云音箱播放不同的提示语音 一个[0,255]的整形值，目前定义如下：                                                                                                                                                          |     |
| 210**WIFI版支持**:1  支付宝 2  微信支付 3  云支付 4  余额支付 5  微信储值 6  微信买单 7  银联刷卡  8  会员卡消费9  会员卡充值10 翼支付11 退款 12 支付宝退款 13 微信退款 14 银行卡退款 15 银联退款 16 工行e支付 18 QQ钱包到账19 京东支付20 用户取消支付22 西银惠支付 | （901、902）**WIFI版支持且仅支持以下前缀**1支付宝收款2微信收款3云闪付收款8会员卡消费9会员卡充值10翼支付收款成功11退款12支付宝退款13微信退款19京东收款成功20有用户取消订单 | *                                                                                                                                                                                                     |     |
| token                                                                                                                                                                          | TOKEN                                                                                                | 代理商的 token, 预先通过安全渠道分配，使得代理商对该 SPEAKERID 有操作权限                                                                                                                                                         | *  |
| version                                                                                                                                                                        | 接口版本                                                                                                 | 按各型号标注的VERSION版本，由用户配置时选择，**预留1-9供选择**                                                                                                                                                                 | *  |
| vol                                                                                                                                                                            | VOLUME                                                                                               | 指音量设置值，范围为 0 到 100，代表从无音到最大声。                                                                                                                                                                          |     |
| seq                                                                                                                                                                            | SEQUENCY                                                                                             | 用于通讯去重复的顺序号，范围为[0,4294967295] (即[0,0xFFFFFFFF])的整数。每次提交时请改变此值（比如按顺序加 1）。 假如服务器在 200 秒（暂定值）内收到两个或多个SEQUENCY 相同、并且提交的内容也相同的请求，则认为是重复提交， 服务器将忽略此提交，并返回错误码 17。此参数缺省时，服务器对此次请求不做去重检查，此次请求也不作为后续去重检查的比较依据。 |     |
| trace_no                                                                                                                                                                       | TRACE_ NUMBER                                                                                       | 代理商用于追踪此支付消息的一个字符串，最大 63个字节，由代理商软件产生。之后代理商可以用此trace_no 通过用“支付消息历史查询接口”查询该条支付消息。此参数对云音箱或服务器工作状态没有影响。                                                                                                    |  * |
| descs                                                                                                                                                                          | DESCRIPTION                                                                                          | 代理商可以给此支付消息一个描述字符串，最大 255个字节。之后代理商用 “支付消息历史查询接口”查询支付消息时，可以看到此描述。此参数对云音箱或服务器工作状态没有影响。                                                                                                                   |     |
| suffix                                                                                                                                                                         | VOLUMESUFFIX                                                                                         | 是否开启自定义收款消息后缀， 1表示开启                                                                                                                                                                                   |     |


<p style="margin-left:0; margin-right:0"><span style="color:#f5222d">备注：</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#f5222d">云音箱收到支付结果后，播放内容为：支付类型 + 金额 </span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">例子：</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#1890ff">https://speaker.17laimai.cn/add.php?id=335&amp;price=3879&amp;token=123456789021</span><span style="color:#1890ff">&amp;version=1</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">表示代理商的</span><span style="color:#262626">&nbsp;token&nbsp;</span><span style="color:#262626">为</span><span style="color:#262626"> </span><span style="color:#262626">123456789021</span><span style="color:#262626">，向</span><span style="color:#262626">&nbsp;id&nbsp;</span><span style="color:#262626">为</span><span style="color:#262626">&nbsp;335&nbsp;</span><span style="color:#262626">的云音箱提交支付金额为</span><span style="color:#262626">&nbsp;38.79&nbsp;</span><span style="color:#262626">元的支付结果</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">3) </span><span style="color:black">返回参数：</span></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">类型</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errcode</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">integer</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回码，参见</span><span style="color:#262626"> </span><span>网关返回码</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errmsg</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">返回码描述</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">detail</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回的数据</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<h2><span>3</span><span>、可选接口</span></h2>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">代理商可根据情况实现可选接口，可选接口不影响云音箱的正常使用。</span></p>

<h3><span>3.1 </span><span>通知语音播报</span><span style="color:#f5222d">（不支持WIFI版，流量版专用）</span></h3>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">将通知消息提交到云音箱服务器、服务器将支付结果推送给云音箱，云音箱接收后播报。</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#f5222d">备注：该接口为流量版（2G\4G）音箱专用接口，通过流量版（2G\4G）音箱自带的TTS播放，WIFI版音箱不可用</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#262626">1</span></strong><strong><span style="color:#262626">）</span></strong><strong><span style="color:#262626">URL</span></strong><strong><span style="color:#262626">：</span></strong><strong><span style="color:#262626">https://speaker.17laimai.cn/notify.php</span></strong><strong><span style="color:#262626"> </span></strong><strong><span style="color:#f5222d">（流量版专用播报接口，流量版可以只用到这一个接口，其它接口选用）</span></strong></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#262626">2</span></strong><strong><span style="color:#262626">）请求参数：</span></strong></p>


| 参数        | 意义             | 解释                                                                                                                                                                                                              | 必须 |   |
| --------- | -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -- | - |
| id        | SPEAKERID      | 指该云音箱标签上的的 SN/ID                                                                                                                                                                                                | * |   |
| token     | 代理商的 token     | 代理商的 token, 预先通过安全渠道分配，使得代理商对该 SPEAKERID 有操作权限                                                                                                                                                                  | * |   |
| version   | 接口版本           | 按各型号标注的VERSION版本，由用户配置时选择，**预留1-9供选择**                                                                                                                                                                          | * |   |
| message   | MESSAGE        | 通知消息内容，长度最长128个字节 [数字处理策略见3.1.1备注](#vjh9s)如果需要断句，则添加逗号“,”                                                                                                                                                       | * |   |
| seq       | SEQUENCY       | 用 于通讯 去重复 的顺序号 ，范围 为 [0,4294967295] ( 即 [0,0xFFFFFFFF])的整数。每次提交时请改变此值（比如按顺序 加 1）。 假如服务器在 200 秒（暂定值）内收到两个或多个 SEQUENCY 相同、并且提交的内容也相同的请求，则认为是重复提交， 将忽略此请求，并返回错误码 17。 此参数缺省时，服务器对此次请求不做去重检查，此次请求 也不作为后续去重检查的比较依据。 |    |   |
| vol       | VOLUME         | 指音量设置值，范围为 0 到 100，代表从无音到最大声。                                                                                                                                                                                   |    |   |
| speed     | SPEED          | 语速，速度范围为0-100，默认为50 (**仅限404、504**)                                                                                                                                                                             |    |   |
| trace_no  | TRACE_ NUMBER | 代理商用于追踪此支付消息的一个字符串，最大 63个字节，由代理商软件产生。之后代理商可以用此trace_no 通过用“支付消息历史查询接口”查询该条支付消息。此参数对云音箱或服务器工作状态没有影响。                                                                                                             |    |   |



<p style="margin-left:0; margin-right:0"><span style="color:black">例子</span><span style="color:black">1</span><span style="color:black">：</span><span style="color:#1890ff">https://speaker.17laimai.cn/notify.php?id=10000091&amp;token=123456789021&amp;version=1&amp;message=你的验证码为</span><span style="color:#1890ff">6688&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">ID</span><span style="color:black">为</span><span style="color:black">10000091</span><span style="color:black">的云音箱播报语音</span><span style="color:black">&nbsp;&ldquo;</span><span style="color:black">你的验证码为</span><span style="color:black">6688&rdquo;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">例子</span><span style="color:black">1</span><span style="color:black">：</span><span style="color:#1890ff">https://speaker.17laimai.cn/notify.php?id=10000091&amp;token=123456789021</span><span style="color:#1890ff">&amp;version=1</span><span style="color:#1890ff">&amp;message=支付宝到账</span><span style="color:#1890ff">120</span><span style="color:#1890ff">元</span><span style="color:#1890ff">,</span><span style="color:#1890ff">实收</span><span style="color:#1890ff">110</span><span style="color:#1890ff">元</span><span style="color:#1890ff">,</span><span style="color:#1890ff">星</span><span style="color:#1890ff">POS</span><span style="color:#1890ff">为你优惠</span><span style="color:#1890ff">10</span><span style="color:#1890ff">元</span><span style="color:#1890ff">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">ID</span><span style="color:black">为</span><span style="color:black">10000091</span><span style="color:black">的云音箱播报语音</span><span style="color:black">&nbsp;&ldquo;</span><span style="color:black">支付宝到账</span><span style="color:black">120</span><span style="color:black">元</span><span style="color:black">,</span><span style="color:black">实收</span><span style="color:black">110</span><span style="color:black">元</span><span style="color:black">,</span><span style="color:black">星</span><span style="color:black">POS</span><span style="color:black">为你优惠</span><span style="color:black">10</span><span style="color:black">元</span><span style="color:black">&rdquo;</span></p>

<h4><span style="color:#f5222d">3.1.1备注：数字处理策略&nbsp;，适用于编号播报，车牌播报等非金额格式的播报。</span></h4>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">当message参数中，数字是按金额来播报的，比如&ldquo;123&rdquo;，播报为&ldquo;一百二十三&rdquo;，如果要按号码、编号来播报，则需要把特殊内容用&ldquo;</span><strong><span style="color:#ff4d4f">[</span></strong><span style="color:#262626">&rdquo;&ldquo;</span><strong><span style="color:#ff4d4f">]</span></strong><span style="color:#262626">&rdquo;方括号包裹起来，</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">比如：</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">1、订单编号</span><strong><span style="color:#ff4d4f">[123]</span></strong><span style="color:#262626">收款66元,则播报为&ldquo;订单编号一二三收款六十六元&rdquo;;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">2、</span><strong><span style="color:#ff4d4f">[津A8526]</span></strong><span style="color:#262626">正常通行，则播报为&ldquo;津A八五二六&rdquo;正常通行</span></p>

<p style="margin-left:0; margin-right:0">&nbsp;</p>

<p style="margin-left:0; margin-right:0"><span style="color:black">3) 返回参数：</span></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">类型</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errcode</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">integer</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回码，参见</span><span style="color:#262626"> </span><span>网关返回码</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errmsg</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">返回码描述</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">detail</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回的数据</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<h3><span>3.2&nbsp;更改语音信息 （</span><span style="color:#8c8c8c">灰度测试</span><span>）</span></h3>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">更改开机语音，自定义播报前缀。</span><strong><span style="color:#f5222d">(</span></strong><span style="color:#f5222d">仅适用于</span><strong><span style="color:#f5222d">402、404、502、504)</span></strong></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#262626">1）URL：https://speaker.17laimai.cn/modify_bootvoicewav.php</span></strong></p>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;&nbsp;</span><span style="color:#d9d9d9"> &nbsp;</span><strong><span style="color:#d9d9d9"> </span></strong></p>

<p style="margin-left:0; margin-right:0"><strong><span style="color:#262626">2</span></strong><strong><span style="color:#262626">）请求参数：</span></strong></p>

****

| 参数       | 意义           | 解释                                                                                                                                                                                                              | 必须 |
| -------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -- |
| id       | SPEAKERID    | 云音箱的 ID                                                                                                                                                                                                         | * |
| token    | TOKEN        | 代理商的 token, 预先通过安全渠道分配，使得代理商对该 SPEAKERID 有操作权限                                                                                                                                                                  | * |
| version  | 接口版本         | 按各型号标注的VERSION版本，**预留1-9供用户配置音箱时选择**                                                                                                                                                                            | * |
| sound    | 开机铃声         | 声音内容中文最长15字其他字节30字节                                                                                                                                                                                             | * |
| off_text | 关机铃声         | 中文，可选                                                                                                                                                                                                           |    |
| type     | TYPE         | 0 表示开机欢迎声音 传 off_text 时此值填写 1                                                                                                                                                                                   | * |
| seq      | SEQUENCY     | 用 于通讯 去重复 的顺序号 ，范围 为 [0,4294967295] ( 即 [0,0xFFFFFFFF])的整数。每次提交时请改变此值（比如按顺序 加 1）。 假如服务器在 200 秒（暂定值）内收到两个或多个 SEQUENCY 相同、并且提交的内容也相同的请求，则认为是重复提交， 将忽略此请求，并返回错误码 17。 此参数缺省时，服务器对此次请求不做去重检查，此次请求 也不作为后续去重检查的比较依据。 |    |
| descs    | DESCRIPTION  | 代理商可以给此绑定请求提供一个描述字符串，最大 255 个 字节。之后代理商用 “ 绑定状态查询接口”查询绑定消息时， 可以看到此描述。 此参数对云音箱或服务器工作状态没有影响。                                                                                                                       |    |


<p style="margin-left:0; margin-right:0"><span style="color:black">例子：</span><span style="color:#1890ff">https://speaker.17laimai.cn/modify_bootvoicewav.php?id=10000091&amp;token=123456789021&amp;sound=欢迎光临&amp;off_text=谢谢使用&amp;type=1&nbsp;&nbsp;&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">表示将云喇叭&nbsp;ID&nbsp;10000091&nbsp;开机语音设置为&nbsp;&ldquo;欢迎光临&rdquo;，关机语音为&ldquo;谢谢使用&rdquo;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">例子：</span><span style="color:#1890ff">https://speaker.17laimai.cn/modify_bootvoicewav.php?id=10000091&amp;token=123456789021&amp;sound=欢迎光临&amp;type=0</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">表示将云喇叭</span><span style="color:black">&nbsp;ID&nbsp;10000091&nbsp;</span><span style="color:black">开机语音设置为</span><span style="color:black">&nbsp;&ldquo;</span><span style="color:black">欢迎光临</span><span style="color:black">&rdquo;</span></p>

<p style="margin-left:0; margin-right:0"><span style="color:black">3) </span><span style="color:black">返回参数：</span></p>

<table border="1" cellspacing="0" style="border-collapse:collapse; border:1px solid #d9d9d9; table-layout:fixed; width:719px">
	<tbody>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">参数</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">类型</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">说明</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">必须</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errcode</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">integer</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回码，参见</span><span style="color:#262626"> </span><span>网关返回码</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">errmsg</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">返回码描述</span><span style="color:black">&nbsp;</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:black">*</span></p>
			</td>
		</tr>
		<tr>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">detail</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">string</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">返回的数据</span></p>
			</td>
			<td style="border-color:#d9d9d9; border-style:solid; border-width:1px; height:24px">
			<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>
			</td>
		</tr>
	</tbody>
</table>

<p style="margin-left:0; margin-right:0"><span style="color:#262626">&nbsp;</span></p>

<p style="margin-left:0; margin-right:0; text-align:justify"><span style="color:black">&nbsp;</span></p>


<h1><span>三、常见问题</span></h1>

<h3><span>1. 此token 无此 SPEAKERID 权限</span></h3>

<p style="margin-left:0; margin-right:0"><span>1）：检查version,是否与当前设备型号对应正确，</span><span>version(接口版本对应表)</span><span>。</span></p>

<p style="margin-left:0; margin-right:0"><span>2）：检查TOKEN是否正确，是否完整</span></p>

<p style="margin-left:0; margin-right:0"><span>3）：联系我们，协助检查。</span></p>

<p style="margin-left:0; margin-right:0">&nbsp;</p>

<p style="margin-left:0; margin-right:0">&nbsp;</p>

<p style="margin-left:0; margin-right:0; text-align:center"><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9c2223a317934d2bbc3e7a8e18d4604c~tplv-k3u1fbpfcp-zoom-1.image" width="193" /></p>

<p style="margin-left:0; margin-right:0; text-align:center"><span>【备注云喇叭】</span><span>&nbsp;</span></p>

<p style="margin-left:0; margin-right:0"><span>&nbsp;</span></p>
