<?php
if (!session_id()) session_start();
$baseinfo['host'] = 'localhost';
$baseinfo['user'] = 'liyuemin';
$baseinfo['pass'] = 'lym71763308';
$baseinfo['data'] = 'new_exam';
$site_name="新蓝职业技能鉴定考试模拟系统";
$site_copy="中国石油大学出版社";
$site_ver="v1.0";
$jibie=array("选择访问级别","初级","中级","高级","技师");
$tixing=array("选择题型","单选题","判断题","多选题","简答题");
$pages=array("20","30","50","100","500");
$conn = new DB1($baseinfo);
header('Content-Type:text/html;charset=utf-8');
mysql_query("set names 'utf8'");
function writeScript($msg)
{
echo "<script>".$msg."</script>";
}
class DB1{
public $type;
public $page;
public function __construct($database){
$this->type = new DB_MYSQL($database);
}
public function execute($sql){
return $this->type->execute($sql);
}
public function getRows($sql,$pageSize=0){
if($pageSize!=0)
{
$page=1;
if(isset($_GET['page']))$page = intval($_GET['page']);
$this->page=$page;
$sql=$sql." limit ".($page-1)*$pageSize.", $pageSize";
}
return $this->type->getRows($sql);
}
public function getRow($sql){
return $this->type->getRow($sql);
}
function getValue($sql)
{
return $this->type->getValue($sql);
}
public function lastID(){
return $this->type->lastID();
}
public function numRows(){
return $this->type->numRows();
}
private function mysqliinstalled(){
if (function_exists("mysqli_connect")) {
return true;
}else{
return false;
}
}
private function escape($sql){
return addslashes($sql);
}
}
class DB_MYSQLi extends DB1{
public $user;
public $pass;
public $host;
public $conn;
public $data;
public $result;
public $mycount;
public function __construct($database){
$this->host = $database['host'];
$this->user = $database['user'];
$this->pass = $database['pass'];
$this->data = $database['data'];
$this->connect();
mysqli_set_charset($this->conn,"utf8");
$this->select();
}
public function connect() {
try {
if (!$this->conn = mysqli_connect($this->host,$this->user,$this->pass)) {
$error  = "Error connection to database.";
throw new Exception($error);
}
}catch (Exception $error){
echo $error->getMessage();
}
}
public function select() {
try {
if (!mysqli_select_db($this->conn,$this->data)) {
$error  = "Error connection to database.";
throw new Exception($error);
}
}catch (Exception $error){
echo $error->getMessage();
}
}
public function execute($sql){
try {
if (!$this->result = mysqli_query($this->conn,$sql)) {
$error = mysqli_error();
throw new Exception($error);
}else{
return $this->result;
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getRows($sql,$pageSize=0){
try {
if (!$result = mysqli_query($this->conn,$sql)) {
$error = mysqli_error();
throw new Exception($error);
}else{
$rows = array();
while ($row = mysqli_fetch_assoc($result)) {
$rows[] = $row;
}
$this->mycount=mysqli_num_rows($result);
$this->free($result);
return $rows;
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getRow($sql){
try {
if (!$result = mysqli_query($this->conn,$sql)) {
$error = mysqli_error();
throw new Exception($error);
}else{
$row = array();
$row = mysqli_fetch_array($result);
$this->mycount=mysqli_num_rows($result);
$this->free($result);
return $row;
}
}
catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getValue($sql){
try {
if (!$result = mysqli_query($this->conn,$sql)) {
$error = mysqli_error();
throw new Exception($error);
}else{
$row = array();
$row = mysqli_fetch_array($result);
$this->free($result);
return $row[0];
}
}
catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function lastID(){
return mysqli_insert_id($this->conn);
}
public function numRows(){
return  	$this->mycount;
}
private function free($result){
if ($result) {
return mysqli_free_result($result);
}
}
}
class DB_MYSQL extends DB1{
public $user;
public $pass;
public $host;
public $conn;
public $data;
public $result;
public $pageCount;
public function __construct($database){
$this->host = $database['host'];
$this->user = $database['user'];
$this->pass = $database['pass'];
$this->data = $database['data'];
$this->connect();
$this->select();
}
public function connect() {
try {
if (!$this->conn = mysql_connect($this->host,$this->user,$this->pass)) {
$error  = "Error connection to database.";
throw new Exception($error);
}
}catch (Exception $error){
echo $error->getMessage();
}
}
public function select() {
try {
if (!mysql_select_db($this->data,$this->conn)) {
$error  = "Error connection to database.";
throw new Exception($error);
}
}catch (Exception $error){
echo $error->getMessage();
}
}
public function execute($sql){
try {
if (!$this->result = mysql_query($sql,$this->conn)) {
$error = mysql_error();
throw new Exception($error);
}else{
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getRows($sql,$pageSize=0){
try {
if (!$result = mysql_query($sql)) {
$error = mysql_error();
throw new Exception($error);
}else{
$rows = array();
while ($row = mysql_fetch_assoc($result)) {
$rows[] = $row;
}
$this->mycount=mysql_num_rows($result);
$this->free($result);
return $rows;
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getRow($sql){
try {
if (!$result = mysql_query($sql)) {
$error = mysql_error();
throw new Exception($error);
}else{
$row = array();
$row = mysql_fetch_array($result);
$this->mycount=mysql_num_rows($result);
$this->free($result);
return $row;
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function getValue($sql){
try {
if (!$result = mysql_query($sql)) {
$error = mysql_error();
throw new Exception($error);
}else{
$row = array();
$row = mysql_fetch_array($result);
$this->free($result);
return $row[0];
}
}catch (Exception $error){
echo $error->getMessage()."<br>$sql";
}
}
public function lastID(){
return mysql_insert_id($this->conn);
}
public function numRows(){
return  	$this->mycount;
}
private function free($result){
if ($result) {
return mysql_free_result($result);
}
}
}
$path_parts = pathinfo($_SERVER['PHP_SELF']);

?>