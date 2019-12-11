# PostgreSQL数据库的迁移支持哪些插件迁移<a name="drs_15_0121"></a>

目前DRS支持将白名单内的插件进行迁移，白名单以外的插件，由于未经测试，存在安全风险，暂不支持迁移。

如果您的插件希望华为RDS for PostgreSQL数据库预支持，请联系技术人员代为提需求给RDS for PostgeSQL内核团队进行处理。

现阶段支持迁移的插件信息请参见[表1](#table2090814290202)。

**表 1**  插件信息

<a name="table2090814290202"></a>
<table><thead align="left"><tr id="row179081529142013"><th class="cellrowborder" valign="top" width="38.080000000000005%" id="mcps1.2.3.1.1"><p id="p2908102917203"><a name="p2908102917203"></a><a name="p2908102917203"></a><strong id="b0641114262019"><a name="b0641114262019"></a><a name="b0641114262019"></a>插件名称</strong></p>
</th>
<th class="cellrowborder" valign="top" width="61.919999999999995%" id="mcps1.2.3.1.2"><p id="p1426851422111"><a name="p1426851422111"></a><a name="p1426851422111"></a><strong id="b1271520209214"><a name="b1271520209214"></a><a name="b1271520209214"></a>描述</strong></p>
</th>
</tr>
</thead>
<tbody><tr id="row290810294201"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p3908129162015"><a name="p3908129162015"></a><a name="p3908129162015"></a>postgis</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p5285331102114"><a name="p5285331102114"></a><a name="p5285331102114"></a>创建postgis时，会同步创建以下插件：</p>
<p id="p52856318214"><a name="p52856318214"></a><a name="p52856318214"></a>postgis</p>
<p id="p2285331132118"><a name="p2285331132118"></a><a name="p2285331132118"></a>postgis_topology</p>
<p id="p32857316213"><a name="p32857316213"></a><a name="p32857316213"></a>fuzzystrmatch</p>
<p id="p20285163117215"><a name="p20285163117215"></a><a name="p20285163117215"></a>postgis_tiger_geocoder</p>
<p id="p13285103142112"><a name="p13285103142112"></a><a name="p13285103142112"></a>address_standardizer</p>
<p id="p1628533182110"><a name="p1628533182110"></a><a name="p1628533182110"></a>address_standardizer_data_us</p>
</td>
</tr>
<tr id="row49089298202"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1329421492210"><a name="p1329421492210"></a><a name="p1329421492210"></a>btree_gin</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p19269121413212"><a name="p19269121413212"></a><a name="p19269121413212"></a>-</p>
</td>
</tr>
<tr id="row19908182911203"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p147995228227"><a name="p147995228227"></a><a name="p147995228227"></a>btree_gist</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1526991452120"><a name="p1526991452120"></a><a name="p1526991452120"></a>-</p>
</td>
</tr>
<tr id="row1909192902010"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p78701730162218"><a name="p78701730162218"></a><a name="p78701730162218"></a>hstore</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p826951432110"><a name="p826951432110"></a><a name="p826951432110"></a>-</p>
</td>
</tr>
<tr id="row11909429182014"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p624023922217"><a name="p624023922217"></a><a name="p624023922217"></a>pg_trgm</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p17269111472118"><a name="p17269111472118"></a><a name="p17269111472118"></a>-</p>
</td>
</tr>
<tr id="row12909102911205"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p15746174714226"><a name="p15746174714226"></a><a name="p15746174714226"></a>tablefunc</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p12269161482110"><a name="p12269161482110"></a><a name="p12269161482110"></a>-</p>
</td>
</tr>
<tr id="row1890902962020"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p10502755162218"><a name="p10502755162218"></a><a name="p10502755162218"></a>unaccent</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1226916146212"><a name="p1226916146212"></a><a name="p1226916146212"></a>-</p>
</td>
</tr>
<tr id="row1190962992011"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p191861538236"><a name="p191861538236"></a><a name="p191861538236"></a>uuid-ossp</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1026912148214"><a name="p1026912148214"></a><a name="p1026912148214"></a>-</p>
</td>
</tr>
<tr id="row49092298203"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p0252414182312"><a name="p0252414182312"></a><a name="p0252414182312"></a>cube</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p02691114152118"><a name="p02691114152118"></a><a name="p02691114152118"></a>-</p>
</td>
</tr>
<tr id="row1193141752313"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1379103482311"><a name="p1379103482311"></a><a name="p1379103482311"></a>dict_int</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1319321714231"><a name="p1319321714231"></a><a name="p1319321714231"></a>-</p>
</td>
</tr>
<tr id="row1667082042313"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1934854312315"><a name="p1934854312315"></a><a name="p1934854312315"></a>dict_xsyn</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p767052013234"><a name="p767052013234"></a><a name="p767052013234"></a>-</p>
</td>
</tr>
<tr id="row1686114235237"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p7861172310232"><a name="p7861172310232"></a><a name="p7861172310232"></a>earthdistance</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p9861123172313"><a name="p9861123172313"></a><a name="p9861123172313"></a>-</p>
</td>
</tr>
<tr id="row1458142652417"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p156298198295"><a name="p156298198295"></a><a name="p156298198295"></a>intagg</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p458152692417"><a name="p458152692417"></a><a name="p458152692417"></a>-</p>
</td>
</tr>
<tr id="row178191828182410"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p2357162372917"><a name="p2357162372917"></a><a name="p2357162372917"></a>intarray</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p188201328112411"><a name="p188201328112411"></a><a name="p188201328112411"></a>-</p>
</td>
</tr>
<tr id="row151091431182418"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p84832244293"><a name="p84832244293"></a><a name="p84832244293"></a>ltree</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1511093112247"><a name="p1511093112247"></a><a name="p1511093112247"></a>-</p>
</td>
</tr>
<tr id="row2068143362418"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p91931125172913"><a name="p91931125172913"></a><a name="p91931125172913"></a>pgcrypto</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p146821533162420"><a name="p146821533162420"></a><a name="p146821533162420"></a>-</p>
</td>
</tr>
<tr id="row159571535192410"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p189579351246"><a name="p189579351246"></a><a name="p189579351246"></a>timescaledb</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p0957135112420"><a name="p0957135112420"></a><a name="p0957135112420"></a>timescaledb插件不支持9.5.5版本的PostgreSQL。</p>
</td>
</tr>
<tr id="row196223712416"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1310132612913"><a name="p1310132612913"></a><a name="p1310132612913"></a>hll</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p179631837122413"><a name="p179631837122413"></a><a name="p179631837122413"></a>-</p>
</td>
</tr>
<tr id="row1696753962410"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1896753916247"><a name="p1896753916247"></a><a name="p1896753916247"></a>zhparser</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p641691119263"><a name="p641691119263"></a><a name="p641691119263"></a>该插件只提供默认词典，不支持用户自定义词典，参数默认值设置如下：</p>
<p id="p64161411112610"><a name="p64161411112610"></a><a name="p64161411112610"></a>zhparser.punctuation_ignore = off</p>
<p id="p11416121102615"><a name="p11416121102615"></a><a name="p11416121102615"></a>zhparser.punctuation_ignore = off</p>
<p id="p5416171102612"><a name="p5416171102612"></a><a name="p5416171102612"></a>zhparser.multi_short = off</p>
<p id="p941621132615"><a name="p941621132615"></a><a name="p941621132615"></a>zhparser.multi_duality = off</p>
<p id="p341661118267"><a name="p341661118267"></a><a name="p341661118267"></a>zhparser.multi_zmain = off</p>
<p id="p441611116261"><a name="p441611116261"></a><a name="p441611116261"></a>zhparser.multi_zall = off</p>
<p id="p14416311122613"><a name="p14416311122613"></a><a name="p14416311122613"></a>zhparser.dict_in_memory = off</p>
</td>
</tr>
<tr id="row9123164262419"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p1091543315298"><a name="p1091543315298"></a><a name="p1091543315298"></a>oracle_fdw，</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1512413427247"><a name="p1512413427247"></a><a name="p1512413427247"></a>仅支持PostgreSQL 10.3连接到Oracle Database 12c或之前的版本。</p>
</td>
</tr>
<tr id="row14554644122417"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p17669123412912"><a name="p17669123412912"></a><a name="p17669123412912"></a>pg_pathman</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p35541844192414"><a name="p35541844192414"></a><a name="p35541844192414"></a>-</p>
</td>
</tr>
<tr id="row2498104762413"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p13400153512296"><a name="p13400153512296"></a><a name="p13400153512296"></a>pg_stat_statements</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1249810471248"><a name="p1249810471248"></a><a name="p1249810471248"></a>-</p>
</td>
</tr>
<tr id="row1075316491243"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p3911336102913"><a name="p3911336102913"></a><a name="p3911336102913"></a>pg_hint_plan</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p1975344922412"><a name="p1975344922412"></a><a name="p1975344922412"></a>-</p>
</td>
</tr>
<tr id="row4981352152416"><td class="cellrowborder" valign="top" width="38.080000000000005%" headers="mcps1.2.3.1.1 "><p id="p780111369298"><a name="p780111369298"></a><a name="p780111369298"></a>pg_jieba</p>
</td>
<td class="cellrowborder" valign="top" width="61.919999999999995%" headers="mcps1.2.3.1.2 "><p id="p19999528243"><a name="p19999528243"></a><a name="p19999528243"></a>-</p>
</td>
</tr>
</tbody>
</table>

