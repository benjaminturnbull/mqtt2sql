# mqtt2sql

This is a fork of [This](https://github.com/curzon01/mqtt2sql)

If in doubt, you should use that version.

The original project stores only the current state for each topic. I had a need to store historic information in 
addition to the most current message. 
This fork changes the database structure to allow this. 

## Installation

Install as directed as per [here](https://github.com/curzon01/mqtt2sql), with the exception of adding the MySQL table. 

The MySQL table should look like:
```
CREATE TABLE `mqtt` (
  `msg_id` BIGINT(20) AUTO_INCREMENT,
	`id`      SMALLINT(5) UNSIGNED NULL DEFAULT NULL,
	`ts`      TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
	`active`  TINYINT(4) NOT NULL DEFAULT '1',
	`topic`   TEXT NOT NULL,
	`value`   LONGTEXT NOT NULL,
	`qos`     TINYINT(3) UNSIGNED NOT NULL DEFAULT '0',
	`retain`  TINYINT(3) UNSIGNED NOT NULL DEFAULT '0',
	PRIMARY KEY (`msg_id` ),
	INDEX `id` (`id`)
)
COLLATE='utf8_general_ci'
ENGINE=InnoDB;


```

