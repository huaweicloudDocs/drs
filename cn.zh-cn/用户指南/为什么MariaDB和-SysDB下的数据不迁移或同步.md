# 为什么MariaDB和 SysDB下的数据不迁移或同步<a name="drs_16_0122"></a>

由于某些MariaDB的版本把SysDB库作为其系统库（类似于MySQL官方版5.7的sys库），所以DRS默认也将SysDB作为所有MariaDB的系统库来处理（等同于MySQL、information\_schema、performance\_schema等库）。如果SysDB确实是业务库，您可以通过工单申请处理。

