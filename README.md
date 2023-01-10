# Pemrograman-Visual

** Create Procedure Table Lowongan **

CREATE PROCEDURE sp_usrdef_lowongan_list 
    @Search varchar(100) = ''
AS 
BEGIN
    SELECT * FROM lowongan  
END 
GO

CREATE PROCEDURE sp_usrdef_lowongan_save 
	@id_lowongan  int = NULL,
    @nama_perusahaan  varchar(50) = NULL ,
    @posisi  varchar(50) = NULL ,
    @kuota  varchar(50) = NULL ,
    @status  varchar(50) = NULL ,
    @pendidikan  varchar(50) = NULL 
AS 
BEGIN
    IF EXISTS(SELECT 1 FROM lowongan WHERE id_lowongan = @id_lowongan ) 
    BEGIN 
        UPDATE lowongan
       SET nama_perusahaan = @nama_perusahaan, 
            posisi = @posisi, 
            kuota = @kuota, 
            status = @status, 
            pendidikan = @pendidikan
        WHERE id_lowongan = @id_lowongan 
    END 
    ELSE 
    BEGIN
        INSERT INTO lowongan (
            nama_perusahaan,
            posisi,
            kuota,
            status,
            pendidikan) 
        VALUES (
            @nama_perusahaan,
            @posisi,
            @kuota,
            @status,
            @pendidikan)
    END
END 
GO

CREATE PROCEDURE sp_usrdef_lowongan_delete 
    @id_lowongan  int = NULL
AS 
BEGIN
    DELETE FROM lowongan WHERE id_lowongan = @id_lowongan 
END 
