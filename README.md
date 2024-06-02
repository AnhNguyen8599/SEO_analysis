# SEO_analysis_code
Search Engine Optimization Analysis
create table seo.uniace (
select email,`Type`,name,title,`MA Referrer`,`IP Address`,`Time`,str_to_date(date_time,'%m/%d/%Y') as datetime
from seo.uni1 u 
union all
select email,`Type`,name,title,`MA Referrer`,`IP Address`,`Time`,str_to_date(date_time,'%m/%d/%Y') as datetime
from seo.uni2 u2
union all
select email,`Type`,name,title,`MA Referrer`,`IP Address`,`Time`,str_to_date(date_time,'%m/%d/%Y') as datetime
from seo.uni3 u3)



/* Create a table that conttains categories of offered online courses*/
create table seo.uni_cat(
select *
from
(
SELECT email,`Type`,name,title,`MA Referrer`,`IP Address`,`Time`,datetime,
  CASE
    WHEN name LIKE '%thực hành%'
      OR name LIKE '%cách tính%'
      OR name LIKE '%cấp độ%'
      OR name LIKE '%tình huống%'
      OR name LIKE '%công thức%'
      or name like '%excel%'
      or name like '%hướng dẫn%'
      OR name LIKE '%làm quen%'
      or name LIKE '%lên ý tưởng%'
      or name LIKE '%vượt qua%'
      or name LIKE '%ứng dụng%'
      or name LIKE '%quản lý%'
      or name LIKE '%phím tắt%'
      or name LIKE '%pivot%'
      or name LIKE '%tùy biến%'
      or name LIKE '%tính năng%'
      or name LIKE '%thành thạo%'
      or name LIKE '%thiết lập%'
      or name LIKE '%bộ nhớ%'
      or name LIKE '%slicer%'
      or name LIKE '%thể hiện%'
      or name LIKE '%nâng cấp%'
      or name LIKE '%điều chỉnh%'
      or name LIKE '%thêm%'
      or name LIKE '%so sánh%'
      or name LIKE '%nhận biết%'
    THEN 'Thực Hành'
    WHEN name LIKE '%dữ liệu%'
      OR name LIKE '%lập trình%'
      OR name LIKE '%data%'
      or name LIKE '%Key%'
      or name LIKE '%PQL%'
      or name LIKE '%power BI%'
      or name LIKE '%intelligence%'
    THEN 'Dữ Liệu'
    WHEN name LIKE '%phân tích%'
      OR name LIKE '%analytics%'
      or name LIKE '%visualization%'
    THEN 'Phân tích'
    WHEN name LIKE '%talent%'
   	  or name LIKE '%young%'
    THEN 'Young Talent'
    WHEN name LIKE '%tài liệu%'
      OR name LIKE '%ngữ cảnh%'
      OR name LIKE '%đọc hiểu%'
      or name LIKE '%cách%'
      or name LIKE '%danh sách%'
      or name LIKE '%tham chiếu%'
      or name LIKE '%tác động%'
      or name LIKE '%women%'
      or name LIKE '%tổng hợp%'
      or name LIKE '%chia sẻ%'
      or name LIKE '%Tổng quan%'
      or name LIKE '%nội dung%'
      or name LIKE '%self%'
      or name LIKE '%lợi ích%'
      or name LIKE '%văn hóa%'
      or name LIKE '%khám phá%'
      or name LIKE '%chỉ số%'
      or name LIKE '%tỉ trọng%'
      or name LIKE '%xu hướng%'
      or name LIKE '%doanh thu%'
      or name LIKE '%lợi ích%'
      or name LIKE 'nguyên tắc%'
      or name LIKE '%yếu tố%'
      or name LIKE '%kỹ năng%'
      or name LIKE '%tại sao%'
      or name LIKE '%ưu điểm%'
      or name LIKE '%tìm hiểu%'
      or name LIKE '%vai trò%'
      or name LIKE '%sự thật'
    THEN 'Tham Khảo'
    WHEN name LIKE '%giao tiếp%'
      or name LIKE '%bản thân%'
      or name LIKE '%đàm phán%'
      or name LIKE '%cảm xúc%'
      or name LIKE '%cách xem%'
    THEN 'Giao Tiếp'
    ELSE 'Khác'
  END AS name_category
FROM seo.uniace) as sub1)

drop table seo.uni_cat 

select name,name_category
from seo.uni_cat
where name_category = 'khác'
group by name
/* Create more columns like school_name, category of mail, hour,..*/
create table seo.uniace_crawl
(
select *, SUBSTRING_INDEX(time, ':', 1) as hour,
	case when `MA Referrer` like '%duckduckgo%' then 'duckduckgo'
	 when `MA Referrer` like '%uniace%' then 'Truc Tiep'
	 when `MA Referrer` like '%coccoc%' then 'Cốc Cốc'
	 when `MA Referrer` like '%facebook%' then 'Facebook'
	 when `MA Referrer` like '%laban%' then 'Laban'
	 when `MA Referrer` like '%sendibt3%' then 'URL link'
	 when `MA Referrer` like '%google%' then 'Google'
	 when `MA Referrer` like '%zalo%' then 'Zalo'
	 when `MA Referrer` like '%yandex%' then 'Yandex'
	 when `MA Referrer` like '%beacons%' then 'Beacons'
	 when `MA Referrer` like '%jotform%' then 'Jotform'
	 when `MA Referrer` like '%ecosia%' then 'Ecosia'
	 when `MA Referrer` like '%messenger%' then 'Facebook'
	 when `MA Referrer` like '%bing%' then 'bing'
	else 'Truc Tiep' 
	end as 'Truy cập từ', 
	case when email like '%gmail%' then 'Ca nhan'
		when email like '%outlook%' then 'Cong Viec'
		when email like '%edu%' then 'Sinh Vien'
	else 'An Danh' end as User_category
from (
select *, 
	case 
		when email like '%st.ueh%' then 'DH Kinh Te HCM'
		when email like '%neu%' then 'DH Kinh Te Quoc Dan'
		when email like '%hcmut%' then 'DH Bach Khoa HCM'
		when email like '%ctu%' then 'DH Can Tho'
		when email like '%uef%' then 'DH Kinh Te Tai Chinh'
		when email like '%ntu%' then 'Nanyan University'
		when email like '%medvnu%' then 'DH Y HCM'
		when email like '%glos.uef%' then 'DH Gloucestershire HCM'
		when email like '%fpt%' then 'DH FPT'
		when email like '%st.phenikaa%' then 'DH Phenikaa'
		when email like '%dau%' then 'DH Kien Truc Da Nang'
		when email like '%hust%' then 'DH Bach Khoa Ha Noi'
		when email like '%hcmiu%' then 'DH Quoc Te HCM'
		When email like '%st.vimaru%' then 'DH Hang Hai Viet Nam'
		When email like '%ptit%' then 'Hoc Vien CN-Buu Chinh-Vien Thong'
		When email like '%nuce%' then 'Hoc Vien CN-Buu Chinh-Vien Thong'
		When email like '%st.buh%' then 'DH Ngan Hang HCM'
		When email like '%utb.edu%' then 'DH Tay Bac'
		When email like '%hanu.edu%' then 'DH Ha Noi'
		When email like '%ftu.edu%' then 'DH Ngoai Thuong'
		When email like '%hoasen%' then 'DH Hoa Sen'
		When email like '%tdc.edu%' then 'Cao Dang CN Thu Duc'
		When email like '%ueb.edu%' then 'DH Kinh Te Ha Noi'
		When email like '%ldxh%' then 'Dh LDXH'
		When email like '%hcmuaf%' then 'DH Nong Lam HCM'
	ELSE 'No Info' end as School_name		
from (
SELECT *,
    CASE
        WHEN email LIKE '%@%' THEN 'Da Dang Ky'
        ELSE 'Chua Dang Ky'
    END AS category_mail
FROM seo.uni_cat uc)as sub) as subbb
)
