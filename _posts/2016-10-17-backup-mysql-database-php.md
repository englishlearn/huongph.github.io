---
layout: blogs_singles
thumbnail: http://cdn.softwaretestinghelp.com/wp-content/qa/uploads/2015/01/Test-oracle-db-backup.jpg
title: PHP - Backup Your MySQL Database Using PHP.
description:  Một trong những nhiệm vụ quan trọng nhất của bất kỳ nhà phát triển cần phải làm thường xuyên là backup cơ sở dữ liệu MySQL của họ. Trong nhiều trường hợp, các cơ sở dữ liệu là gì ổ đĩa nhất của trang web. Trong khi hầu hết các máy chủ web làm một bản sao lưu hàng ngày của cơ sở dữ liệu của khách hàng, dựa vào họ để thực hiện sao lưu và cung cấp cho họ miễn phí là nguy hiểm để nói rằng ít nhất. Đó là lý do tại sao tôi đã tạo ra một chức năng sao lưu cơ sở dữ liệu mà tôi có thể gọi bất cứ khi nào tôi muốn - bao gồm CRONs hàng đêm.
date: 17 Oct 2016
author: Huongph
---

Một trong những nhiệm vụ quan trọng nhất của bất kỳ nhà phát triển cần phải làm thường xuyên là backup cơ sở dữ liệu MySQL của họ. Trong nhiều trường hợp, các cơ sở dữ liệu là quan trọng của trang web. Trong khi hầu hết các máy chủ web làm một bản sao lưu hàng ngày của cơ sở dữ liệu của khách hàng, dựa vào họ để thực hiện sao lưu và cung cấp cho họ miễn phí là nguy hiểm để nói rằng ít nhất. Đó là lý do tại sao tôi đã tìm được một chức năng trên net tạo ra một chức năng sao lưu cơ sở dữ liệu mà tôi có thể gọi bất cứ khi nào tôi muốn - bao gồm CRONs hàng đêm.

{% highlight javascript %}
{% raw %}
<?php
	backup_tables('localhost','username','password','blog');

/* backup the db OR just a table */
function backup_tables($host,$user,$pass,$name,$tables = '*')
{
	
	$link = mysql_connect($host,$user,$pass);
	mysql_select_db($name,$link);
	
	//get all of the tables
	if($tables == '*')
	{
		$tables = array();
		$result = mysql_query('SHOW TABLES');
		while($row = mysql_fetch_row($result))
		{
			$tables[] = $row[0];
		}
	}
	else
	{
		$tables = is_array($tables) ? $tables : explode(',',$tables);
	}
	
	//cycle through
	foreach($tables as $table)
	{
		$result = mysql_query('SELECT * FROM '.$table);
		$num_fields = mysql_num_fields($result);
		
		$return.= 'DROP TABLE '.$table.';';
		$row2 = mysql_fetch_row(mysql_query('SHOW CREATE TABLE '.$table));
		$return.= "\n\n".$row2[1].";\n\n";
		
		for ($i = 0; $i < $num_fields; $i++) 
		{
			while($row = mysql_fetch_row($result))
			{
				$return.= 'INSERT INTO '.$table.' VALUES(';
				for($j=0; $j < $num_fields; $j++) 
				{
					$row[$j] = addslashes($row[$j]);
					$row[$j] = ereg_replace("\n","\\n",$row[$j]);
					if (isset($row[$j])) { $return.= '"'.$row[$j].'"' ; } else { $return.= '""'; }
					if ($j < ($num_fields-1)) { $return.= ','; }
				}
				$return.= ");\n";
			}
		}
		$return.="\n\n\n";
	}
	
	//save file
	$handle = fopen('db-backup-'.time().'-'.(md5(implode(',',$tables))).'.sql','w+');
	fwrite($handle,$return);
	fclose($handle);
}
?>

